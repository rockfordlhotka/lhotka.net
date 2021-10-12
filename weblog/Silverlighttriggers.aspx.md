---
title: Silverlight triggers
postDate: 2009-08-14T13:44:31.8171843-05:00
abstract: 
postStatus: publish
---
14 August 2009

Based on my recent posts regarding Silverlight, MVVM and invoking methods on arbitrary target objects, a couple people suggested that behaviors or trigger actions might be a good solution.

These are new concepts introduced through the System.Windows.Interaction assembly that comes with Expression Blend 3. That’s somewhat of a drawback, since this means a developer is required to install Blend 3 to get the assembly before these features are available. It would be nicer if they were part of the standard Silverlight (and WPF) development platform.

The other challenge I’ve encountered in working with this technology is a limitation when it comes to data binding. Silverlight only full binds with dependency properties of FrameworkElement objects. Since classes like TriggerAction&lt;T&gt; don’t inherit from FrameworkElement, their dependency properties aren’t bindable. This means you can’t define a property on a trigger and then bind it to other elements in the UI, which is really an unfortunate limitation.

For example, I created an [Execute trigger action](http://www.lhotka.net/cslacvs/viewvc.cgi/trunk/cslalightcs/Csla/Silverlight/Execute.cs?revision=4141&amp;view=markup) that defines MethodName and MethodParameter properties. If I have a ListBox and a Button, and I want the Button to trigger some method that acts on the SelectedItem property of the ListBox, what I’d really like to do is this:


> &lt;Button Content="Refresh"&gt;
>   &lt;i:Interaction.Triggers&gt;
>     &lt;i:EventTrigger EventName="Click"&gt;
>       &lt;csla:Execute MethodName="Load" **MethodParameter="{Binding ElementName=MyListBox, Path=SelectedItem}"** /&gt;
>     &lt;/i:EventTrigger&gt;
>   &lt;/i:Interaction.Triggers&gt;
> &lt;/Button&gt;


(in this code the ‘i’ prefix refers to System.Windows.Interactivity from Blend 3 and the ‘csla’ prefix refers to Csla.Silverlight from CSLA .NET)

Unfortunately this won’t get past the Silverlight XAML parser, because a binding expression isn’t allowed for MethodParameter…

I also wanted to implement a MethodTarget property so the Execute trigger could invoke methods on some object other than the current DataContext. Unfortunately that puts us back to needed the ability to use binding to specify the value of MethodTarget, which isn’t possible. So my current implementation can only invoke methods on the DataContext of the associated control (the Button in this case).

To get around the MethodParameter limitation I’m using a Tag hack


> &lt;Button Content="Refresh" **Tag="{Binding ElementName=NewIdTextBox, Path=Text}"**&gt;
>   &lt;i:Interaction.Triggers&gt;
>     &lt;i:EventTrigger EventName="Click"&gt;
>       &lt;csla:Execute MethodName="Load" /&gt;
>     &lt;/i:EventTrigger&gt;
>   &lt;/i:Interaction.Triggers&gt;
> &lt;/Button&gt;


When the Execute trigger invokes the method, it passes an [ExecuteEventArgs parameter](http://www.lhotka.net/cslacvs/viewvc.cgi/trunk/cslalightcs/Csla/Silverlight/ExecuteEventArgs.cs?revision=4141&amp;view=markup) to the method, which includes a TriggerSource property of type FrameworkElement. This means the method, in the view model class, can access the Tag property of the associated control (the Button), which *can be bound* because the Button is a FrameworkElement:


> public void Load(object sender, ExecuteEventArgs e)
> {
>   var tag =** e.TriggerSource.Tag**.ToString();
>   int id = 0;
>   if (!string.IsNullOrEmpty(tag))
>     id = int.Parse(tag);
>   Load(id);
> }


Sure this is somewhat hacky, but since the trigger action can’t define bindable properties of its own, this seems like a workable solution.
