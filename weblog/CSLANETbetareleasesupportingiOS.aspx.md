---
title: CSLA .NET beta release supporting iOS
postDate: 2014-03-17T23:42:21.2187036-05:00
abstract: 
postStatus: publish
---
17 March 2014

I just created a release of CSLA 4 version 4.5.580-Beta with preliminary support for iOS via the [Xamarin](http://www.xamarin.com) tools.

You can get it via nuget (easiest), or from the [release page on GitHub](https://github.com/MarimerLLC/csla/releases/tag/4.5.580-Beta).

This is an exciting pre-release because it now means you can reuse the same business logic code across all modern app client platforms and the desktop and the cloud. This is a “who’s who” list of supported platforms:

- iOS
    - iPad
    - iPhone
- Android
    - Phones
    - Tablets
- Windows
    - WinRT (Windows 8)
    - WPF
    - Silverlight
    - Windows Forms
- Windows Phone
- Cloud and servers
    - Windows Azure
    - Windows Server
    - ASP.NET (MVC and Web Forms)
    - WCF
    - Web API
- Linux
- OS X


[CSLA .NET](http://www.cslanet.com/) allows you to easily create reusable business logic (authorization, validation, calculations, etc.) and to share a common app server with simple network configuration. I don’t know of any other open source C# framework that makes it possible for you to reuse *the exact same business logic* across all these different platforms.

Because the iOS support is new we are asking for your help. If you have the [Xamarin](http://xamarin.com/) tools for iOS *please* help us out by building some business code using CSLA and let us know if you find any issues (either on the forum at http://forums.lhotka.net or via the [CSLA GitHub page](https://github.com/MarimerLLC/csla).
