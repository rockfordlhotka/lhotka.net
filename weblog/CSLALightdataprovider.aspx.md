---
title: CSLA Light data provider
postDate: 2008-08-13T12:03:32.137-05:00
abstract: 
postStatus: publish
---
13 August 2008

WPF has this cool concept called a data provider control. CSLA .NET includes a custom data provider control that enables nearly codeless forms (if you don't count XAML as code), by supporting the following functions purely through XAML:

1. Create/Fetch an object
2. Save an object
3. Cancel changes to an object
4. Add a new item to a list (if the object is a collection)
5. Remove an item from a list (if the object is a collection)


Silverlight doesn't have a data provider concept, nor does it have *commanding*. Which means that you need to write code behind the form for all of those actions.

So in CSLA Light we're investigating the possibility of some sort of data provider control to fill in this gap. The idea is that you'd be able to declare a CslaDataProvider as a resource on your form and use it as a data source, and as a handler for the save/cancel/add/remove operations.

This also means we need a way, through XAML, to route things like a button's Click event to methods on CslaDataProvider (because there's no commanding in Silverlight).

At a prototype level what we've got is something like this. The CslaDataProvider goes in the Resources section just like it would in WPF:


> &lt;UserControl.Resources&gt;
>   &lt;csla:CslaDataProvider x:Key="MyData"
>                                      ManageObjectLifetime="True" /&gt;
> &lt;/UserControl.Resources&gt;


Some WPF concepts don't make sense. For example, IsAsynchronous is useless because in Silverlight it *will be asynchronous*. Others, like IsInitialLoadEnabled might make sense, we're not entirely sure yet.

Your page XAML then uses this as a data source. But where WPF does some magic behind the scenes for data providers, Silverlight doesn't know about data providers. So you have to deal with this yourself when setting the DataContext:


> &lt;Grid x:Name="LayoutRoot" DataContext="{Binding Source={StaticResource MyData}, Path=Data}"&gt;


The DataContext is set to use the Data property of the data provider, because that's where the actual business object is found. In WPF this indirection is hidden automatically, but in Silverlight you have to do it yourself.

In the Form\_Loaded() method in code behind you call your business object's factory method. But rather than handling the async callback yourself, you allow the data provider to handle it:


> private void Form\_Loaded(...)
> {
>   var dp = (CslaDataProvider)this.Resources["MyData"];
>   CustomerEdit.GetCustomer(123, dp.FetchCompleted);
> }


I hope to eliminate even this bit of code behind (at least for parameterless create/fetch scenarios), but the current prototype does require it. The CslaDataProvider exposes a set of async handlers for create and fetch operations.

When the async request completes, the CslaDataProvider object's Data property changes to reflect the new business object. That causes a PropertyChanged event, which in turn causes data binding to refresh the UI so the user sees the data.

That gets us pretty close to the WPF data provider capability of creating or retrieving an object. But the Csla.Wpf.CslaDataProvider goes further, and so the plan is for the Csla.Silverlight.CslaDataProvider to also go further.

The data provider object has methods like Save() and Cancel() that can be called to save the object or cancel changes. The trick then, is how to get UI elements, like a button, to call those methods when Silverlight has no commanding or relative binding.

At the moment we're addressing this with an InvokeMethod object that exposes some attached properties. So you can create a Button like this:


> &lt;Button csla:InvokeMethod.Resource="{StaticResource MyData}"
>              csla:InvokeMethod.MethodName="Save"
>              csla:InvokeMethod.TriggerEvent="Click"
>              Content="Save" /&gt;


This tells the InvokeMethod object to listen for a Click event from the Button. When it gets a Click event, it invokes the Save() method on the MyData resource. Any RoutedEventHandler or EventHander event can be handled, which should cover nearly all events from any type of UI control. The Button control's Click event, for example, is a RoutedEventHandler, as are most Silverlight control events.

(this is only possible btw, thanks to the relaxed delegate support in the current versions of C# and VB)

The same technique will work to call Cancel(), and presumably AddNewItem() and RemoveItem() at some point (though with RemoveItem() we'll also need a way to pass in a parameter value to specify the item to be removed).

The result is that we're pretty close, at least in concept, to the WPF data provider model, and we avoid the need to write code behind the form for common events like save, cancel, add new and remove.
