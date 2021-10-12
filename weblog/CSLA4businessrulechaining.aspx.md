---
title: CSLA 4 business rule chaining
postDate: 2010-04-05T23:51:46.96-05:00
abstract: 
postStatus: publish
---
05 April 2010

I knew I was forgetting something when I wrote the [big post](http://www.lhotka.net/weblog/CSLA4BusinessRulesSubsystem.aspx) covering the new CSLA .NET business rule system. And it was rule chaining, which really is a big feature.

In CSLA 3.8 a rule could return one value: true or false. This is because a rule was a Boolean method. Oh sure, you could return some limited data through the RuleArgs (Description, Severity, StopProcessing), but this was really all part of one result.

In CSLA 4 a rule can return many results. This means that one rule can invoke other rules, and all their consolidated results are returned as the result of the one rule. Or you could create a rule that invoked an external rules engine, returning all results of the engine as a result of your rule. Or you could create a rule that invoked a workflow (as in Windows Workflow Foundation 4), again consolidating the results of the workflow as a result of your rule.

One way to use this is as an escape hatch. If you don’t like the way CSLA manages rules, just write your own “rule” that is actually a replacement rule engine, and allow CSLA to invoke your rule engine every time a property changes.

But even if you don’t go so far as to write your own rule engine, there are various interesting patterns that fit neatly within the existing CSLA 4 rule model.

For example, it is quite common for people to want to invoke a rule only if other properties of the object are in a certain state. Maybe you only want to require a value if the object is new, but not if it already exists. To do this, you can create a gate rule


> public class NewGateRule : BusinessRule
> {
>   public NewGateRule(Csla.Core.IPropertyInfo primaryProperty)
>     : base(primaryProperty)
>   { }
>
> private IBusinessRule \_innerRule =
>     (IBusinessRule)new Csla.Rules.CommonRule.Required(PrimaryProperty);
>
> protected override void Execute(RuleContext context)
>   {
>     var obj = context.Target as Csla.Core.ITrackStatus;
>     if (obj != null && obj.IsNew)
>       \_innerRule.Execute(context.GetChainedContext(required));
>   }
> }


This rule creates an instance of the Required rule, but only executes that inner rule if the target business object’s IsNew property is true. So the real rule is only invoked if the gate condition is met.

Notice the use of the GetChainedContext() method, which takes the RuleContext passed to the NewGateRule and creates a chained RuleContext that is appropriate for the inner rule. This technique automatically consolidates the results of the inner rule together with the outer rule (and any other chained rules) so when the NewGateRule completes all the results are automatically processed.

The same coding technique could be used to invoke many other rules if desired, each one having its own chained RuleContext. And chaining can be nested, so you could have a gate rule execute another gate rule that executes the real rule and that should work fine.

Keeping in mind that rules are just types, it is possible to do something slightly more dynamic – though your metadata does need to include not just the full type name of the rule, but also a way to describe the constructor parameters required. But this pseudo-code illustrates the concept:


> public class DynamicRule : BusinessRule
> {
>   public DynamicRule(Csla.Core.IPropertyInfo primaryProperty, string innerRule)
>     : base(primaryProperty)
>   {
>     var t = Type.GetType(innerRule);
>     object[] args = new object[] { primaryProperty };
>     \_innerRule = (IBusinessRule)Activator.CreateInstance(t, args);
>   }
>
> private IBusinessRule \_innerRule;
>
> protected override void Execute(RuleContext context)
>   {
>     \_innerRule.Execute(context.GetChainedContext(required));
>   }
> }


In this case the rule expects the full type name of the real rule to be provided. It uses that type information to dynamically create an instance of the real rule, and then executes it using a chained RuleContext. It should be clear that this basic concept could be extended to create a rule that dynamically loads an entire set of rules (perhaps using MEF) and executes those rules using chaining.
