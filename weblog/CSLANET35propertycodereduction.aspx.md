---
title: CSLA .NET 3.5 property code reduction
postDate: 2008-02-28T21:25:11.726-06:00
abstract: 
postStatus: publish
---
28 February 2008

One of my primary goals with [CSLA .NET 3.5](http://www.lhotka.net/cslanet) was to reduce the amount of code necessary for common business object tasks - like declaring a property or implementing a parent-child relationship. I've mentioned what I'm doing on the forum and elsewhere, but I thought a summary blog post would be nice. I'm motivated, because I spent some time earlier today upgrading some business object code based on CSLA 3.0.3 to 3.5 and it was just fun to watch the class shrink :)

### Basic Properties

Prior to 3.5 my properties were comparatively large:


> public string Name
> {
>   [System.Runtime.CompilerServices.MethodImpl(System.Runtime.CompilerServices.MethodImplOptions.NoInlining)]
>   get
>   {
>     CanReadProperty(true);
>     return \_name;
>   }
>   [System.Runtime.CompilerServices.MethodImpl(System.Runtime.CompilerServices.MethodImplOptions.NoInlining)]
>   set
>   {
>     CanWriteProperty(true);
>     if (value == null) value = string.Empty;
>     if (\_name != value)
>     {
>       \_name = value;
>       PropertyHasChanged();
>     }
>   }
> }


Now the same property looks like this:


> private static PropertyInfo&lt;string&gt; NameProperty =
>   RegisterProperty&lt;string&gt;(typeof(CertificationEdit), new PropertyInfo&lt;string&gt;("Name"));
> public string Name
> {
>   get { return GetProperty&lt;string&gt;(NameProperty); }
>   set { SetProperty&lt;string&gt;(NameProperty, value); }
> }


I think that is so cool!! Though there's a performance hit to this much reduction, because you'll notice there's no backing field. In this case CSLA is actually managing the property value in the background and that incurs a little overhead. You can compromise if you'd like:


> private static PropertyInfo&lt;string&gt; NameProperty =
>   RegisterProperty&lt;string&gt;(typeof(CertificationEdit), new PropertyInfo&lt;string&gt;("Name"));
> private string \_name = NameProperty.DefaultValue;
> public string Name
> {
>   get { return GetProperty&lt;string&gt;(NameProperty, \_name); }
>   set { SetProperty&lt;string&gt;(NameProperty, ref \_name, value); }
> }


Nearly the same code, but now with a private backing field so CSLA doesn't have to manage the value. Slightly faster, with slightly more code.

Either way, all the authorization, validation and data binding support works just like it did with the old syntax, so all the core features of CSLA .NET just keep working in your favor - with less code to write and maintain.

### Child Object Properties

This new syntax works for child objects as well. A child used to look like this:


> private ChildType \_child;
> public ChildType Child
> {
>   [System.Runtime.CompilerServices.MethodImpl(System.Runtime.CompilerServices.MethodImplOptions.NoInlining)]
>   get
>   {
>     CanReadProperty(true);
>     return \_child;
>   }
> }


The new syntax *requires* that CSLA manage the property value for child objects:


> private static PropertyInfo&lt;ChildType&gt; ChildProperty =
>   RegisterProperty&lt;ChildType&gt;(typeof(CertificationEdit), new PropertyInfo&lt;string&gt;("Child"));
> public ChildType Child
> {
>   get { return GetProperty&lt;ChildType&gt;(ChildProperty); }
> }


The really cool part isn't the minor code savings in the property - it is the code savings elsewhere. Prior to 3.5 a parent object had to override IsDirty and IsValid, and had to hook and re-hook child data binding events. *None of that code is required now!* Because CSLA is managing the child object value, it can entirely handle IsDirty, IsValid and all data binding events automatically. This saves a *lot* of code in every parent object.

Even better, this eliminates code that a lot of people forgot to write, or forgot to update when adding a new child. In short, this eliminates a primary source of bugs/pain when dealing with parent-child object relationships.

There are other areas in 3.5 where I've reduced the code required, and I'll blog about others (like reducing data access code, eliminating many criteria classes and more) in future posts.
