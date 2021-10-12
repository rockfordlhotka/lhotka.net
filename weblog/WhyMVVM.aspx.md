---
title: Why MVVM?
postDate: 2011-10-03T10:59:08.8805212-05:00
abstract: 
postStatus: publish
---
03 October 2011

People often ask “Why should I use MVVM? It seems like it complicates things.”

The most common reason hard-core developers put forward for MVVM is that “it enables unit testing of presentation code”.

Although that can be true, I don’t think that’s the *primary* reason people should invest in MVVM.

I think the primary reason is that it protects your presentation code against some level of change to the XAML. It makes your code more maintainable, and will help it last longer.

For example, build a WPF app with code-behind. Now try to move it to Silverlight without changing any code (only XAML). Pretty hard huh?

Or, build a Silverlight app with code-behind. Now have a user experience designer rework your XAML to look beautiful. Your app won’t build anymore? They changed numerous XAML types and there are now compiler errors? Oops…

Looking forward, try taking any WPF or Silverlight app that has code-behind and moving it to WinRT (Windows 8) without changing any code (only XAML – and the XAML *will* need to change). Turns out to be nearly impossible doesn’t it?

And yet, I have lots of CSLA .NET application code that uses MVVM to keep the presentation code cleanly separated from the XAML. Examples where the *exact same code* runs behind WPF and Silverlight XAML. I’m not quite yet to the point of having CSLA working on WinRT, but I fully expect *the exact same code* to run on Windows 8, just with a third set of XAML.

To me, that is the power and value of MVVM. Your goal should be no code-behind, viewmodel code that doesn’t rely on specific XAML types, and an abstract set of viewmodel methods that can be bound to arbitrary UI events.

Yes, MVVM is an investment. But it will almost certainly pay for itself over time, as you maintain your app, and move it from one flavor of XAML to another.

Does MVVM mean you can *completely* avoid changing code when the XAML changes? No. But it is a whole lot closer than any other technique I’ve seen in my 24+ year career.
