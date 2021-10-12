---
title: Implementing an async rule in CSLA 4 version 4.5
postDate: 2012-10-09T16:59:52.2936836-05:00
abstract: 
postStatus: publish
---
09 October 2012

CSLA 4 version 4.5 supports the async and await keywords across all platforms (WinRT, .NET 4.5, .NET 4, Silverlight 5).

You can use these async features to implement async rules in the CSLA rules engine. Here’s one such rule:


> public class CustomRule : Csla.Rules.BusinessRule
> {
>   public CustomRule(Csla.Core.IPropertyInfo primaryProperty)
>     : base(primaryProperty)
>   {
>     InputProperties.Add(primaryProperty);
>     IsAsync = true;
>   }
>
> protected async override void Execute(Csla.Rules.RuleContext context)
>   {
>     var cmd = new LongRunningCommand();
>     cmd = await DataPortal.ExecuteAsync(cmd);
>     context.AddInformationResult("Rule complete: " + cmd.Output);
>     context.Complete();
>   }
>
> [Serializable]
>   public class LongRunningCommand : CommandBase&lt;LongRunningCommand&gt;
>   {
>     public static readonly PropertyInfo&lt;string&gt; OutputProperty = RegisterProperty&lt;string&gt;(c =&gt; c.Output);
>     public string Output
>     {
>       get { return ReadProperty(OutputProperty); }
>       private set { LoadProperty(OutputProperty, value); }
>     }
>
> protected new async Task DataPortal\_Execute()
>     {
>       Output = "Before delay";
>       await Task.Delay(3000);
>       Output = "After delay";
>     }
>   }
> }


Notice that the rule’s constructor sets the rule’s IsAsync property to true. This tells the CSLA rules engine that the rule will be async.

Also notice that the rule’s Execute method is marked with the async keyword, allowing the use of the await keyword within the method. In this example, the rule uses the data portal to asynchronously execute a command object by awaiting the ExecuteAsync method.

Because the rule has IsAsync true, the Execute method *must* call context.Complete to indicate that the rule has finished processing. If you don’t call context.Complete the CSLA rule engine will never process the rule’s result, and you’ll have a bug in your application.

The command object itself also uses the async keyword to implement the DataPortal\_Execute method. Notice that this method returns a Task. The server-side data portal components are smart enough to detect when a DataPortal\_XYZ method returns type Task, so the DataPortal\_XYZ method is invoked correctly.

Within the DataPortal\_Execute method I just use Task.Delay to create an artificial delay. This represents some long-running operation such as calling a slow web service, invoking an intensive oData query, or something like that.

The end result is that a business object can attach this CustomRule to a property, and the rule will run asynchronously. This is done in the business class’s AddBusinessRules method.

In your UI you can use helper components such as Csla.Xaml.PropertyInfo to determine that the property is running an async rule. For example, you might use XAML like this in WinRT:


> &lt;StackPanel Orientation="Horizontal"&gt;
>   &lt;TextBox Text="{Binding Path=Name, Mode=TwoWay}"/&gt;
>   &lt;TextBlock Text="{Binding ElementName=NameInfo,Path=RuleDescription}" Foreground="Yellow"/&gt;
>   &lt;ProgressRing IsActive="{Binding ElementName=NameInfo,Path=IsBusy}"/&gt;
>   &lt;csla:PropertyInfo Name="NameInfo" Source="{Binding}" Property="Name"/&gt;
> &lt;/StackPanel&gt;


The specific XAML syntax is a little different in WPF/Silverlight because the XAML language is more mature there than in WinRT. But the basic concept of building a rich user experience based on an async rule is the same across all smart client platforms.
