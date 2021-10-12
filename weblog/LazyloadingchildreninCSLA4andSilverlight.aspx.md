---
title: Lazy loading children in CSLA 4 and Silverlight
postDate: 2010-07-01T13:11:43.551-05:00
abstract: 
postStatus: publish
---
01 July 2010

The fact that server access is all async in Silverlight makes some common tasks a little more challenging. This includes lazy loading child objects in an on-demand manner.

When implementing lazy loading in CSLA it is pretty typical to implement the on-demand load of the child property value in the child property getter. In other words, in the parent object, there’ll be a property that exposes the child object, and in the getter of that property is where the lazy loading code goes:


> public static PropertyInfo&lt;Child&gt; ChildProperty = RegisterProperty&lt;Child&gt;(c =&gt; c.Child);
> public Child Child
> {
>   get
>   {
> **    if (!FieldManager.FieldExists(ChildProperty))
>     {
>       Child = DataPortal.Fetch&lt;ChildLoader&gt;().Child;
>       OnPropertyChanged(ChildProperty);
>     }
> **    return GetProperty(ChildProperty);
>   }
>   private set { LoadProperty(ChildrenProperty, value); }
> }


The ChildLoader type shown here is a command object (I typically use a ReadOnlyBase subclass) that runs to the server, loads the child object and returns it to the client. ChildLoader might look like this:


> [Serializable]
> public class ChildLoader : ReadOnlyBase&lt;ChildLoader&gt;
> {
>   public static PropertyInfo&lt;Child&gt; ChildProperty = RegisterProperty&lt;Child&gt;(c =&gt; c.Child);
>   public Child Child
>   {
>     get { return ReadProperty(ChildProperty); }
>     private set { LoadProperty(ChildProperty, value); }
>   }
>
>   private void DataPortal\_Fetch()
>   {
>     Child = DataPortal.FetchChild&lt;Child&gt;();
>   }
> }


This all works great in .NET, where all this code is synchronous. But it needs a little tweaking to work in Silverlight, where server communication is async.

First, the parent property getter must return something *before it has the actual value*. This is kind of a big deal, because it means the UI must be able to handle getting back a null value, and then later getting the real value. This isn’t too hard though, at least if you are using data binding, because the UI will show nothing for the null value, and will automatically refresh the display when the real value arrives (because CSLA will raise a PropertyChanged event for the Child property).

Also, you’ll probably want to mark the parent object as busy while the operation is occurring, so the UI can take appropriate steps (again, by using data binding against the IsBusy property) to block the user from trying to interact with this part of the app until the actual data arrives:


> public static PropertyInfo&lt;Child&gt; ChildProperty = RegisterProperty&lt;Child&gt;(c =&gt; c.Child);
> public Child Child
> {
>   get
>   {
> **    if (!FieldManager.FieldExists(ChildProperty))
>     {
>       MarkBusy();
>       DataPortal.BeginFetch&lt;ChildLoader&gt;((o, e) =&gt;
>         {
>           if (e.Error != null)
>             throw e.Error;
>           Child = e.Object.Child;
>           MarkIdle();
>           OnPropertyChanged(ChildProperty);
>         });
>     }
> **    return GetProperty(ChildrenProperty);
>   }
>   private set { LoadProperty(ChildrenProperty, value); }
> }


When the getter is first called it will start the async load operation, and then it will return null. Later, when the BeginFetch() call completes it will set the Child property to the actual value and indicate that the parent object is no longer busy.

The ChildLoader is unaffected, since it was (and still is) running primarily on the .NET app server. The only difference is that the client is using BeginFetch() instead of Fetch(), so the ChildLoader is running async instead of sync. But that doesn’t affect the way ChildLoader works – so the only impact is to the parent object’s Child property getter.
