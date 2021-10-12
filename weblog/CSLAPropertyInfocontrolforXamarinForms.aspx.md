---
title: CSLA PropertyInfo control for Xamarin Forms
postDate: 2016-05-26T16:57:07.5594223-05:00
abstract: 
postStatus: publish
---
26 May 2016

[![th7JTBT6D7](binary/Open-Live-Writer/CSLA-PropertyInfo-control-for-Xamarin-Fo_EDD4/th7JTBT6D7_thumb.jpg "th7JTBT6D7")](binary/Open-Live-Writer/CSLA-PropertyInfo-control-for-Xamarin-Fo_EDD4/th7JTBT6D7_2.jpg)There is now a Csla.Xaml.PropertyInfo control for Xamarin Forms as well as WPF/UWP, so you can use the same technique to access all metastate about each property from your XAML.

This means that (now on Xamarin too) you can bind to the property value, as well as CanRead, CanWrite, IsValid, IsBusy, and various other metastate values.

Using this capability your XAML UI can provide the user with immediate and rich visual cues as to whether the user is allowed to read or write the property value, and whether the current property value is valid (and if not, why), as well as whether the property has any outstanding async business rules currently executing.

In short, all the goodness that WPF/Silverlight/UWP developers have enjoyed over the past many years is now available on Xamarin!

(or will be once CSLA .NET 4.6.400 releases in about a week – though you can try it now with the 4.6.400 prerelease available via NuGet)
