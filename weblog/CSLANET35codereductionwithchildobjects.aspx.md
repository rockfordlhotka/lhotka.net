---
title: CSLA .NET 3.5 code reduction with child objects
postDate: 2008-03-10T23:15:41.724-05:00
abstract: 
postStatus: publish
---
10 March 2008

In a previous post I talked about the new property declaration syntax options in CSLA .NET 3.5. When it comes to child objects, if the shortest form is used then CSLA will pretty much completely take care of all parent-child object interaction so you don't have to do it by hand. This is a tremendous code savings!

So declaring a child property like this:


> private static PropertyInfo&lt;ChildList&gt; ChildListProperty =
>   RegisterProperty&lt;ChildList&gt;(new PropertyInfo&lt;ChildList&gt;("ChildList");
> public ChildList ChildList
> {
>   get { return GetProperty&lt;ChildList&gt;(ChildListProperty); }
> }


allows CSLA to manage the child object. Of course you do need to create the child object somewhere, such as in the DataPortal\_XYZ methods:


> [RunLocal]
> private void DataPortal\_Create()
> {
>   // initialize other fields here
>   LoadProperty&lt;ChildList&gt;(ChildListProperty, ChildList.NewList());
>   base.DataPortal\_Create();
> }
>
> private void DataPortal\_Fetch(...)
> {
>   // initialize other fields here
>   LoadProperty&lt;ChildList&gt;(ChildListProperty, ChildList.GetList(this.Id));
> }


Another option is to use a lazy loading scheme. There are a couple options in how you can use lazy loading. You can avoid the DataPortal\_Create() implementation by just creating a new, empty list - and I do this almost all the time now:


> private static PropertyInfo&lt;ChildList&gt; ChildListProperty =
>   RegisterProperty&lt;ChildList&gt;(new PropertyInfo&lt;ChildList&gt;("ChildList");
> public ChildList ChildList
> {
>   get
>   {
> **    if (!FieldManager.FieldExists(ChildListProperty))
>       SetProperty&lt;ChildList&gt;(ChildListProperty, ChildList.NewList());
> **    return GetProperty&lt;ChildList&gt;(ChildListProperty);
>   }
> }


With this approach you still need to load the child data in the DataPortal\_Fetch() method. The only thing this does is eliminate the need for the code in DataPortal\_Create() - which often means you don't need DataPortal\_Create() at all.

Another option is to truly lazy load the object by calling a factory method that actually loads the object with existing data:


> private static PropertyInfo&lt;ChildList&gt; ChildListProperty =
>   RegisterProperty&lt;ChildList&gt;(new PropertyInfo&lt;ChildList&gt;("ChildList");
> public ChildList ChildList
> {
>   get
>   {
>     if (!FieldManager.FieldExists(ChildListProperty))
> **      SetProperty&lt;ChildList&gt;(ChildListProperty, ChildList.GetList(this.Id));
> **    return GetProperty&lt;ChildList&gt;(ChildListProperty);
>   }
> }


Obviously this requires that the ChildList class implement a GetList() factory that calls the data portal so it can be loaded independently from its parent. This is different from the first example, where GetList() would use the new child data portal support (or could be implemented the old 3.0 way). I'll discuss the new child data portal support in a future blog post.

If you use lazy loading, CSLA will automatically ensure that the newly created child has its edit level set correctly and that all data binding events cascade appropriately.

in all cases you no longer need to write code in a parent object like this:


> <font color="#800000">protected override bool IsDirty<br>{<br>&nbsp; get<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; return base.IsDirty || _childList.IsDirty;<br>&nbsp; }<br>}<br><br>protected override bool IsValid<br>{<br>&nbsp; get<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; return base.IsValid &amp;&amp; _childList.IsValid;<br>&nbsp; }<br>}</font>


Nor do you need to do any hooking of child object events like PropertyChanged or ListChanged - that's all automatic as well.
