---
title: WPF 4.0 Data Binding Fix
postDate: 2009-05-27T10:28:10.65543-05:00
abstract: 
postStatus: publish
---
27 May 2009

Since WPF came out there’s been one quirk, one “optimization” in data binding that has been a serious pain.

Interestingly enough the same quirk is in Windows Forms, but the WPF team tells me that the reason it is also in WPF is entirely independent from how and why it is in Windows Forms.

The “optimization” is that when a user changes a value in the UI, say in a TextBox, that value is then put into the underlying source object’s property (whatever property is bound to the Text property of the TextBox). If the source object *changes the value in the setter* the change will never appear in the UI. Even if the setter raises PropertyChanged, WPF ignores it and leaves the original (bad) value in the UI.

To overcome this, you’ve had to put a ValueConverter on every binding expression in WPF. In CSLA .NET I created an IdentityConverter, which is a value converter that does nothing, so you can safely attach a converter to a binding when you really didn’t want a converter there at all, but you were forced into it to overcome this WPF data binding quirk.

WPF 4.0 fixes the issue. Karl Shifflett describes the change very nicely in [this blog post](http://karlshifflett.wordpress.com/2009/05/27/wpf-4-0-data-binding-change-great-feature/).

This should mean that I can remove the (rather silly) IdentityConverter class from CSLA .NET 4.0, and that makes me happy.
