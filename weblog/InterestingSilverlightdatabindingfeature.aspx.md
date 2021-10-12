---
title: Interesting Silverlight data binding &ldquo;feature&rdquo;
postDate: 2009-01-28T15:35:02.222-06:00
abstract: 
postStatus: publish
---
28 January 2009

I just ran into an odd “feature” of Silverlight data binding, that I assume must actually be a bug.

I have an object with a string property that has a public get, but private set:


> public string Name
> {
>   get { return GetProperty(NameProperty); }
>   private set { SetProperty(NameProperty, value); }
> }


You would think that no code outside the business class could call the set block, because it is private. Certainly in .NET this would appear as a read-only property to any code outside the class.

But in Silverlight, data binding is perfectly capable of calling this code. Worse, the reflection PropertyInfo object for this property returns true for CanWrite, so this appears as a read-write property to any code.

I don’t think the problem is in the C# compiler, because if I write code that tries to set the property I get a compile-time error saying that’s not allowed.

Also, it isn’t a problem with reflection, because trying to set the value using the SetValue() method of a PropertyInfo object fails with the expected MethodAccessException (Silverlight reflection doesn’t allow you to manipulate private members). This, in particular, is weird, because if CanWrite returns true it should be safe to write to a property…


> **Update: **I just checked .NET (being the suspicious sort) and it turns out that CanWrite returns true for a read-only set block in .NET too. And of course reflection won't set the property due to the scope issue, just like SL. But WPF data binding also doesn't call the private set block, where Silverlight somehow cheats and does call it - so at least the scope of the issue is narrowed a bit.


Which begs the question then: how is data binding bypassing the normal property scope protections so it can manipulate a private member? With the next question being how can I do it too? :)

Seriously, this is the first time I’ve found where Microsoft has code in Silverlight that totally bypasses the otherwise strict rules, and it is a bit worrisome (and a pain in the @$$).

Anyway, the workaround at the moment is to use the old-fashioned approach and create a separate mutator method:


> public string Name
> {
>   get { return GetProperty(NameProperty); }
> }
>
> private void SetName(string value)
> {
>   SetProperty(NameProperty, value);
> }


This works, because when there’s no set block at all the property is actually read-only to everyone, inside and outside the class. Kind of inconvenient for the other code inside the business class that wants to set the property, because that code must use this non-standard mutator method – but at least it works…
