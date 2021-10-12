---
title: Win8, Metro, and WinRT terminology
postDate: 2011-10-14T22:04:37.0807377-05:00
abstract: 
postStatus: publish
---
14 October 2011

With all the new terminology and conceptual surface area that comes with the OS code-named “Windows 8”, I’ve been struggling to come up with clarity as I discuss the technology. In the absence of true clarity from Microsoft, we’re left to interpret that they’ve said and come up with our own consistent terminology.

Here’s my current thinking:

- Windows 8 – the new operating system that runs in a “dual mode”: Desktop (Win32) and WinRT
- Win32 – the OS API that supports today’s applications in Win8
- WinRT – the new OS API that supports future applications
- Metro – a user experience design language often used when building WinRT applications


If I’m right, this is important, because people will ultimately be building business applications on WinRT. Those apps may or may not be strictly “Metro”, but by running on WinRT they’ll gain the benefits of the new runtime API, services, and application model.

People talk about “Metro apps”, but even in the Microsoft samples there are apps running on WinRT that violate those standards left and right. So it is *extremely clear* that WinRT apps might or might not be “Metro”.

Additionally, it seems pretty reasonable to think about building Silverlight or WPF apps, even today, following the Metro standards. Some of that might require a lot of work (at least until third party control vendors create some new components for us), but it is surely possible.

So you could argue that "Metro apps” might transcend WinRT. In fact, Metro is also used to describe Windows Phone apps, and they are mostly written in Silverlight.

So I think there are “WinRT apps”, and this includes any/all apps written on the WinRT API.

Then there are “Metro apps” that are probably a WinRT app, that also follows the Metro user experience guidelines.

This terminology helps a lot when talking about .NET, present and future.

Right now, today, we have some flavors of .NET:

- .NET Full profile
- .NET Client profile
- Silverlight
- Windows Phone


It seems to me that Windows 8 just adds a new option:

- .NET WinRT profile


As I think about the future of CSLA .NET, for example, this is how I approach the issue. We’ve already put in a lot of work to make the framework support the existing flavors of .NET (plus mono, mono for iOS, and mono for Android). Much of that effort lays the necessary groundwork for also supporting this new WinRT flavor of .NET.
