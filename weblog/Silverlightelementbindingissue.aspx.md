---
title: Silverlight element binding issue
postDate: 2009-08-04T22:13:49.4311659-05:00
abstract: 
postStatus: publish
---
04 August 2009

I’m trying to do something that seems like it should be so simple and obvious.

I have an attached property, MethodParameter, which I’m applying to a Button, but I’m binding to a ListBox control:


> &lt;Button Content="Process items"
>         csla:InvokeMethod.TriggerEvent="Click"
>         csla:InvokeMethod.MethodName="ProcessItems"
>         csla:InvokeMethod.MethodParameter="{Binding ElementName=DataListBox, Path=SelectedItems}"/&gt;


This works, and does bind. But it appears to bind only when the Button control is instantiated, not when the Click event is handled.

In other words, the binding occurs. The user then interacts with the ListBox control and selects some items, and then clicks the Button. That triggers the Click event, which causes the InvokeMethod object to actually use the MethodParameter value.

However, at that point in time the binding appears to still be using the original collection from when the form was being loaded, and so the collection is empty.

If I actually examine the SelectedItems property it has multiple items of course – but it is a different collection than the one from when the form was loaded.

In other words, ListBox seems to create a whole new collection each time SelectedItems is invoked, and that’s apparently totally messing up data binding.

I don’t know if this problem is unique to ListBox, or if it is a broader problem with element binding, but it is making my life very unpleasant…

To solve this, I’m hijacking the binding process like this:


> public static object GetMethodParameter(UIElement ctrl)
> {
>   var fe = ctrl as FrameworkElement;
>   if (fe != null)
>   {
>     var be = fe.GetBindingExpression(MethodParameterProperty);
>     var dataItem = be.DataItem;
>     string path = be.ParentBinding.Path.Path;
>     if (dataItem != null && !string.IsNullOrEmpty(path))
>     {
>       var pi = Csla.Reflection.MethodCaller.GetProperty(dataItem.GetType(), path);
>       return Csla.Reflection.MethodCaller.GetPropertyValue(dataItem, pi);
>     }
>   }
>   return ctrl.GetValue(MethodParameterProperty);
> }


Basically I’m using reflection to manually go get the property value of the target object. This works, but feels really wrong.

If we’re dealing with a nasty idiosyncrasy of the ListBox I can probably restrict this to only be messy when talking to a ListBox control, but I rather suspect ListBox isn’t the only issue.

I’ve tried all sorts of things on the binding expression - Mode=TwoWay and BindsDirectlyToSource=True. But they had no impact. It appears that the binding gets a reference to the property value when it is created and never knows enough to re-read the value later when I actually need it.

Any ideas?
