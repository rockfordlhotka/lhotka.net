---
title: CSLA 4 Authorization Rules
postDate: 2010-04-24T00:07:27.8930637-05:00
abstract: 
postStatus: publish
---
24 April 2010

I’m well into the redesign of the authorization system in CSLA .NET. The new system is integrated into the new business rules system, and so is no longer a separate concept. To me this makes sense, since authorization rules are just a specific type of business rule.

Some of the basic concepts from CSLA .NET 2.0 to 3.8 are still there. Per-property authorization:

- CanReadProperty()
- CanWriteProperty()
- CanExecuteMethod()


Per-type authorization (which is a little different now) where you can ask:

- Can the user create an instance of this type?
- Can the user get/fetch an instance of this type?
- Can the user edit/save an instance of this type?
- Can the user delete an instance of this type?


And the new per-instance authorization where you can ask:

- Can the user create the instance you already have? (silly, but possible)
- Can the user get/fetch the instance you already have? (silly, but possible)
- Can the user edit/save this instance?
- Can the user delete this instance?


The actual authorization checks occur by executing an IAuthorizationRule rule object. CSLA provides the AuthorizationRule base class to make it easy to implement most rules, and includes IsInRole and IsNotInRole rules. For example, here’s the IsInRole rule:


> /// &lt;summary&gt;
> /// IsInRole authorization rule.
> /// &lt;/summary&gt;
> public class IsInRole : AuthorizationRule
> {
>   private List&lt;string&gt; \_roles;
>
> /// &lt;summary&gt;
>   /// Creates an instance of the rule.
>   /// &lt;/summary&gt;
>   /// &lt;param name="action"&gt;Action this rule will enforce.&lt;/param&gt;
>   /// &lt;param name="roles"&gt;List of allowed roles.&lt;/param&gt;
>   public IsInRole(AuthorizationActions action, List&lt;string&gt; roles)
>     : base(action)
>   {
>     \_roles = roles;
>   }
>
> /// &lt;summary&gt;
>   /// Creates an instance of the rule.
>   /// &lt;/summary&gt;
>   /// &lt;param name="action"&gt;Action this rule will enforce.&lt;/param&gt;
>   /// &lt;param name="element"&gt;Member to be authorized.&lt;/param&gt;
>   /// &lt;param name="roles"&gt;List of allowed roles.&lt;/param&gt;
>   public IsInRole(AuthorizationActions action, Csla.Core.IMemberInfo element, List&lt;string&gt; roles)
>     : base(action, element)
>   {
>     \_roles = roles;
>   }
>
> /// &lt;summary&gt;
>   /// Rule implementation.
>   /// &lt;/summary&gt;
>   /// &lt;param name="context"&gt;Rule context.&lt;/param&gt;
>   protected override void Execute(AuthorizationContext context)
>   {
>     if (\_roles.Count &gt; 0)
>     {
>       foreach (var item in \_roles)
>         if (Csla.ApplicationContext.User.IsInRole(item))
>         {
>           context.HasPermission = true;
>           break;
>         }
>     }
>     else
>     {
>       context.HasPermission = true;
>     }
>   }
> }


At its most basic a rule is composed of some simple items:

- An action (read/write property, execute method, create/get/edit/delete type/instance)
- An optional target element (property/method)
- An Execute() method that actually implements the rule


If your rule needs more information that’s fine – it is your class, so you can just add more properties. Just remember that a rule object is used across all instances of a business object type, so (just like with other business rules) the Execute() method *absolutely must not change instance-level state in the rule object*.

The Execute() method is passed a context object. The context object contains some simple properties:

1. Target (optional reference to business object)
2. HasPermission (true/false result returned by rule)


The Target property may be null. For per-property rules it will not be null, and for per-instance rules it will not be null. But for per-type rules it will be null. The way CSLA itself (especially the data portal) invokes rules is always per-property or per-type. The thing is, when possible even the per-type checks include the Target reference (typically only for CanEditObject checks). So you can use it if it is there, but you need to handle the case where it is null.

But the real point here, is that you can write your own authorization rule that has nothing to do with roles. You could use permissions, claims, random numbers – whatever you want to use to decide whether the user can or can’t perform the requested action.

Authorization rules are added in the AddBusinessRules() override in your business class – just like other business rules:


> protected override void AddBusinessRules()
> {
>   BusinessRules.AddRule(new IsInRole(
>     AuthorizationActions.WriteProperty,
>     NameProperty,
>     new List&lt;string&gt; { “Administrator” });
> }


The rule set concept from other business rules applies here too – so you can have different authorization rules for different users/contexts/etc.

Finally, you can invoke rules as follows:


> // per-type
> bool result = Csla.Rules.BusinessRules.HasPermission(
>   AuthorizationActions.CreateObject, typeof(Customer));
> // per-instance
> bool result = Csla.Rules.BusinessRules.HasPermission(
>   AuthorizationActions.EditObject, \_myCustomer);


The existing IAuthorizeReadWrite interface continues to operate as in 3.x, so you can use that to invoke CanReadProperty/CanWriteProperty/CanExecuteMethod as before.
