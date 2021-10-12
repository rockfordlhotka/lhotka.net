---
title: CSLA 4 business rules subsystem
postDate: 2010-04-05T13:40:05.900675-05:00
abstract: 
postStatus: publish
---
05 April 2010

The first preview of the new CSLA 4 business rules subsystem will be available soon from http://www.lhotka.net/cslanet/download.aspx.

Of course there are a lot of other changes to CSLA .NET in this preview, so make sure to carefully read the change log. Although there are a lot of breaking changes, most of them have pretty minimal impact on people who are already using the 3.8 coding style for classes. Except for the business rules – that impacts everyone.

This is a major change to the way business and validation rules work, with some pretty amazing new capabilities as a result.

The next preview will roll authorization rules into this as well, and that’ll be the last major change for CSLA 4.

The business rule changes apply to both Silverlight and .NET – as always the idea is that the vast majority of your business code should be the same regardless of platform.

I’d like to summarize the primary changes from 3.8 to 4 in regards to business and validation rules.

## Simple changes

The simplest change is that the ValidationRules property in BusinessBase is now named BusinessRules. Also, the Csla.Validation namespace has been replaced by the Csla.Rules namespace.

If you are using DataAnnotations validation attributes in 3.8, they continue to work in 4 without change.

That was the easy part. Now for the interesting changes.

## Rule classes

Rule methods are replaced by rule classes. This means a 3.8 rule like this:


> private static bool MyRule&lt;T&gt;(T target, RuleArgs e) where T : Customer
> {
>   if (target.Sales &lt; 10)
>   {
>     e.Description = "Customer has low sales";
>     e.Severity = RuleSeverities.Information;
>     return false;
>   }
>   else
>     return true;
> }


becomes a class like this:


> private class MyRule : Csla.Rules.BusinessRule
> {
>   protected override void Execute(RuleContext context)
>   {
>     var target = (Customer)context.Target;
>     if (target.Sales &lt; 10)
>       context.AddInformationResult("Customer has low sales");
>   }
> }


It is the same basic rule, but packaged just a little differently. Rule types must implement IBusinessRule, but it is easier to inherit from BusinessRule, which provides a set of basic functionality you’ll typically need when implementing a rule.

The most important thing to understand is that the RuleContext parameter provides input and output for the Execute() method. The context parameter includes a bunch of information necessary to implement the rule, and has methods like AddErrorResult() that you use to indicate the results of the rule.

There’s one coding convention that you must follow: the protected properties from BusinessRule *must never be changed in Execute()*. I wish .NET had the ability to create an immutable type – a class where you could initialize properties as the object is created, and then ensure they are never changed after that point. But such a concept doesn’t exist, at least in C# or VB. But that is what you must do with rule objects. You can set the properties of the rule object as it is created. After that point, if you change properties of the rule object you are going to cause bugs. So do not change the properties of a rule in Execute() and you’ll be happy.

## AddRule Method

In the Customer business class you still override AddBusinessRules(), and that code looks like this:


> protected override void AddBusinessRules()
> {
>   base.AddBusinessRules();
>   BusinessRules.AddRule(new MyRule { PrimaryProperty = SalesProperty });
> }


The new AddRule() method accepts an instance of an IBusinessRule instead of a delegate like in 3.8. This one instance of the rule is used for all instances of the business object type. In other words, exactly one instance of MyRule is created, and it is used by all instances of Customer. You must be aware of this when creating a rule class, because it means you can *never alter instance-level fields or properties after the rule is initialized*. If you do alter an instance-level field or property, you’ll affect the rule’s behavior for all Customer objects in the entire application – and that’d probably be a very bad thing.

Most rule methods that require a primary property will actually require it on the constructor. For example, look at the Required and MaxLength rules:


> protected override void AddBusinessRules()
> {
>   base.AddBusinessRules();
>   BusinessRules.AddRule(new MyRule { PrimaryProperty = SalesProperty });
> **  BusinessRules.AddRule(new Csla.Rules.CommonRules.Required(NameProperty));
>   BusinessRules.AddRule(new Csla.Rules.CommonRules.MaxLength(NameProperty, 20));
> **}


The result is the same either way, but when you are writing your rules it is typically best to explicitly require a primary property on the constructor if you plan to use the primary property value. Later I’ll talk about per-object rules that have no primary property.

You should also notice that the properties are always Csla.Core.IPropertyInfo, not string property names. The new business rule system*requires* that you use PropertyInfo fields to provide metadata about your properties. This syntax has been available since CSLA 3.5, and for my part I haven’t created a business class without them for years. This is one part of a larger effort to eliminate the use of string property names throughout CSLA and CSLA-based business code.

## Invoking Rules

In the previous AddRule() call, the PrimaryProperty property of the rule is set to SalesProperty. This is what links the rule to a specific property. So when the Sales property changes, this rule will be automatically invoked. As in 3.8, all rules are invoked (by default) when an object is created through the data portal, and can be invoked by calling BusinessRules.CheckRules(). And you can invoke rules for a property with BusinessRules.CheckRules(SalesProperty) – though you should notice that CheckRules() now requires an IPropertyInfo, not a string property name.

If you don’t provide a PrimaryProperty value as shown in this example, the rule method is associated with the business type, not a specific property. This means that the rule will run when CheckRules() is called with no parameter, or when the new CheckObjectRules() method is called to invoke rules attached to the business type.

In summary, there are now three CheckRules() overloads:

1. CheckRules() – checks all rules for an object
2. CheckObjectRules() – checks all rules not associated with a specific property (object rules)
3. CheckRules(property) – checks all rules for a specific property


The same concepts of priority and short-circuiting from 3.8 apply in 4.

## InputProperties and InputPropertyValues

You can write that same rule just a little differently, making it unaware of the Target object reference:


> public class MyRule : Csla.Rules.BusinessRule
> {
>   public MyRule(Csla.Core.IPropertyInfo primaryProperty)
>     : base(primaryProperty)
>   {
>     InputProperties = new List&lt;Csla.Core.IPropertyInfo&gt; { primaryProperty };
>   }
>
> protected override void Execute(RuleContext context)
>   {
>     var sales = (double)context.InputPropertyValues[PrimaryProperty];
>     if (sales &lt; 10)
>       context.AddInformationResult("Sales are low");
>   }
> }


This is a little more complex and a lot more flexible. Notice that the rule now requires a primary property, which is actually managed by the BusinessRule base class. Also notice that it adds the primaryProperty value to a list of InputProperties. This tells CSLA that any time this rule is invoked, it must be provided with that property value.

In the Execute() method notice how the sales value is retrieved from the context by using the InputPropertyValues dictionary. This dictionary contains the values from the business object based on the properties in the InputProperties list. A rule can require many property values be provided. Of course the rule will only work with objects that actually have those properties!

Because this rule will work with any object that can provide a double property value, the class is now public and could be placed in a library of rules.

The AddRule() method call in Customer must change a little:


> protected override void AddBusinessRules()
> {
>   base.AddBusinessRules();
>   BusinessRules.AddRule(new MyRule(SalesProperty));
> }


As before, the PrimaryProperty property is being set, but this time it is through the constructor instead of setting the property directly. This is because the rule now requires the primary property value, and can only work if it is supplied.

## Business Rules: Rules that modify data

The CSLA 4 rules system formally supports business rules. Really 3.8 did too, but it was a little confusing with the terminology, which is why ValidationRules is now called BusinessRules – to avoid that confusion.

The RuleContext object now has an AddOutValue() method you can use to provide an output value from your rule:

context.AddOutValue(NameProperty, “Rocky”);

When the rule completes, any out values are updated into the business object using the LoadProperty() method (so there’s no circular loop triggered).

This AddOutValue() technique is safe for synchronous and asynchronous rules, because the business object isn’t updated until the rule completes and control has returned to the UI thread.

If you are creating a synchronous rule, the RuleContext does have a Target property that provides you with a reference to the business object, so you could set the property yourself – just remember that setting a property typically triggers validation, which could cause an endless loop. Overall, it is best to use AddOutValue() to alter values.

## Validation Rules: Errors, Warnings and Information

As in 3.8, CSLA 4 allows validation rules to provide an error, a warning or an informational message. The RuleContext object has three methods:

1. AddErrorResult()
2. AddWarningResult()
3. AddInformationalResult()


Each of these methods takes a string parameter which is the human-readable text to be displayed. A rule should only call one of these methods. If the rule calls them more than once, only the last one will have effect.

If AddErrorResult() is called, the rule is returning a failure result, and the business object will become invalid (IsSelfValid will be false).

If no method is called, or AddWarningResult() or AddInformationalResult() is called the rule is returning a success result and the business object will not become invalid. This is basically the same as the 3.8 behavior.

## Dependent Properties

The concept of dependent properties is quite different in the new system. Instead of an AddDependentProperty() method, a rule now indicates the properties it affects. This can be coded into the rule itself or specified when AddRule() is called. Either way, what’s happening is that every rule object maintains a list of AffectedProperties for that rule.

When a rule completes a PropertyChanged event is raised for every property in AffectedProperties, as well as any properties altered through AddOutValue().

It is also important to realize that, with an async rule, all properties in AffectedProperties will be marked busy when the rule starts, which typically means the user will see a busy animation (if you are using the PropertyStatus control) to show that the property has some outstanding operation running.

## Rule Sets

This is a major new feature of the rules system that is designed to support web applications where multiple customers/clients/organizations are sharing the same virtual root and application. In that case it might be necessary to have different business rules for each customer/client/organization. Rule sets are a way to accomplish this goal.

When you call BusinessRules.AddRule(), the rules are added to a rule set. Normally they are added to the default rule set, and if you only need one set of rules per type of object you can just be happy – it works. But if you need multiple sets of rules per type of object (such as one set of rules for customer A and a different set for customer B), then you’ll want to load each set of rules and attach those rules to your business object type.

This is done by changing the BusinessRules.RuleSet property. For example:


> protected override void AddBusinessRules()
> {
>   base.AddBusinessRules();
>
> // add rules to default rule set
>   BusinessRules.AddRule(...);
>   BusinessRules.AddRule(...);
>   BusinessRules.AddRule(...);
>
> // add rules to CustA rule set
>   BusinessRules.RuleSet = "CustA";
>   BusinessRules.AddRule(...);
>   BusinessRules.AddRule(...);
>   BusinessRules.AddRule(...);
>
> // add rules to CustB rule set
>   BusinessRules.RuleSet = "CustB";
>   BusinessRules.AddRule(...);
>   BusinessRules.AddRule(...);
>   BusinessRules.AddRule(...);
>
>   // use default rule set
>   BusinessRules.RuleSet = “default”;
> }


This code loads rules into three rule sets: default, CustA and CustB. It is up to you to set the RuleSet property to the correct value for each business object instance.

To set the rule set, set the BusinessRules.RuleSet property, then make sure to call BusinessRules.CheckRules() to apply the new set of rules.

The RuleSet value is serialized along with the state of the business object, so you can (and typically will) set the RuleSet property in your DataPortal\_Create() and DataPortal\_Fetch() methods, and that rule set will be used through the life of the object. I expect the most common scenario will be to set the RuleSet based on the identity of the current user, or some context value in Csla.ApplicationContext.ClientContext.

## Per-Object Rules

Finally, it is possible to have rules that are not attached to a specific primary property. These rules are attached to the business object. For example:


> protected override void AddBusinessRules()
> {
>   base.AddBusinessRules();
>   BusinessRules.AddRule(new MyObjectRule());
> }
>
> private class MyObjectRule
> {
>   protected override void Execute(RuleContext context)
>   {
>     var target = (Customer)context.Target;
>     // check rules here
>   }
> }


Notice that the AddRule() method has no primary property specified. Because there’s no primary property, the rule is attached to the business object itself. Normally this type of rule is a private rule in the business class, and uses the business object’s properties directly. But you can specify input and affected properties, as well as provide output values as discussed earlier.

Per-object rules are run in two cases:

- You call BusinessRules.CheckRules()
- You call BusinessRules.CheckObjectRules()


Per-object rules are not run automatically when properties change. So if you don’t invoke them, they won’t run.

## Async Rules

One of my primary goals in designing the new rule system is to provide a lot of consistency between sync and async rules. To this end, both sync and async rules are constructed the same way: by implementing IBusinessRule or subclassing BusinessRule.

But there are some extra restrictions on async rules. Most notably, async rules must get their input values through the RuleContext, and must provide any output values through RuleContext. To help enforce this, the context.Target property is always null in an async rule. This should help prevent the rule from trying to interact directly with the business object.

The reason this is so important, is that I assume an async rule will run some of its code on a background thread. Most of CSLA (and .NET) is not threadsafe, so having multiple threads interact with a business object will cause problems. If the async rule uses the RuleContext as a message to get and return values, CSLA can help ensure processing occurs on the correct thread.

Here’s a simple async rule. It is a little silly, in that all it does is ToUpper() a string value, but it should give you the idea:


> public class AsyncToUpper : Csla.Rules.BusinessRule
> {
>   public AsyncToUpper(Csla.Core.IPropertyInfo primaryProperty)
>     : base(primaryProperty)
>   {
>     IsAsync = true;
>     InputProperties = new List&lt;Csla.Core.IPropertyInfo&gt; { primaryProperty };
>   }
>
> protected override void Execute(Csla.Rules.RuleContext context)
>   {
>     var bw = new System.ComponentModel.BackgroundWorker();
>     bw.DoWork += (o, e) =&gt;
>     {
>       var value = (string)context.InputPropertyValues[PrimaryProperty];
>       context.AddOutValue(PrimaryProperty, value.ToUpper());
>     };
>     bw.RunWorkerCompleted += (o, e) =&gt;
>     {
>       if (e.Error != null)
>         context.AddErrorResult(e.Error.Message);
>       context.Complete();
>     };
>     bw.RunWorkerAsync();
>   }
> }


The rule indicates that it is async by setting IsAsync to true in its constructor. This tells CSLA that the rule expects to run some or all of its logic on a background thread, so CSLA does some extra work for you. Specifically, CSLA marks the primary property and any AffectedProperties as busy before the rule starts and not busy when it ends. It also sets up the rule invocation so its results are handled through an async callback within CSLA. And it makes sure the RuleContext.Target property is null.

Next, notice that the InputProperties list is initialized in the rule’s constructor. This is the list of property values the rule requires to operate, and these property values will be provided through the RuleContext to the Execute() method in the InputPropertyValues dictionary.

The Execute() method itself is using a BackgroundWorker to run some code on a background thread. You can use BackgroundWorker or the async DataPortal and they’ll work fine. The one big requirement here is that whatever you use *must ensure that the competed callback is on the UI thread*. It is *your responsibility* to make sure the completed callback is on the UI thread (if any). The BackgroundWorker and data portal do this for you automatically. If you use some other async technology you must take steps to make sure this is done correctly.

The AddOutValue() method is used to provide the output value. Remember that the actual business object property isn’t affected until after the rule completes, which is when CSLA is handling the results of your rule on the UI thread (where it can safely update the business object).

The RunWorkerCompleted event is used to handle any async errors. You’d do the same thing with the data portal, handling the FetchCompleted event (or similar). It is important to remember that exceptions occurring on a background thread are lost unless you carry them through. The code shown here is following what I typically do, which is to add an error result from the rule in the case of an async exception.

One last thing to keep in mind: there is exactly one instance of your rule object being used by all instances of a business type. Because of this, the Execute() method must be atomic and stateless. To put it another way, you should never, ever, ever alter any instance-level fields or properties of the rule object from the Execute() method. If you do alter an instance-level field or property of the rule object, that change will affect *all business objects*, not just the one you are running against right now. And with async rules you’ll run into race conditions and other nasty multi-threading issues. This is really the same restriction I mentioned earlier with sync rules – don’t change rule properties in Execute() – but it is so important that I wanted to reiterate the point here too.

While there are some restrictions on how you construct an async rule, I am pretty happy with how similar sync and async rules are to implement. In fact, all the async concepts (input values, AddOutValue()) work just fine with sync rules too.

## Moving from 3.8 to 4

While the new business rules system is somewhat different from the 3.8 implementation, the process of moving from 3.8 to 4 isn’t terribly painful.

- Every rule method must become a rule class. This is a pretty mechanical process, but obviously does require some work
- Every use of ValidationRules must be changed to BusinessRules
- Every AddRule() call will be affected, which is another mechanical change
- Dependent properties become AffectedProperties on each AddRule() method call


I was able to get the entire unit test codebase changed over in less than 8 hours – and that included changes not only for the business rules, but also for the data portal and several other breaking changes. I don’t mean to trivialize the effort required, but the changes are mostly mechanical in nature, so it is really a matter of plowing through the code to make the changes, which is mostly repetitive and boring, not really hard.

## Summary

I’m using the major version change from 3 to 4 as an opportunity to make some fairly large changes to CSLA. Changes that enable some key scenarios needed by [Magenic](http://www.magenic.com/) customers, and requested by people on the [forum](http://forums.lhotka.net/) explicitly or implicitly. Some effort will be required to upgrade, but I suspect most people will find it well worth the time.

The big changes are:

- Rule sets
- Per-object rules
- Rule objects instead of rule methods
- Common model for sync and async rules


I’m pretty excited about these changes, and I hope you find them useful!
