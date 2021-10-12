---
title: CSLA 4 version 4.5.600 release with iOS support
postDate: 2014-06-18T15:34:52.9568395-05:00
abstract: 
postStatus: publish
---
18 June 2014

[![csla win8_full](binary/WindowsLiveWriter/CSLA4version4.5.600releasewithiOSsupport_DB1C/csla%20win8_full_thumb.png "csla win8_full")](binary/WindowsLiveWriter/CSLA4version4.5.600releasewithiOSsupport_DB1C/csla%20win8_full_2.png) This release adds the following key features:

1. Support for iOS
2. Support for WinRT on Windows Phone 8.1
3. Support for Universal Apps that target WinRT on Windows 8.1 and Windows Phone 8.1
4. A new HttpProxy/Host data portal channel that doesn't rely on WCF
5. A new BrokeredProxy/Host data portal channel that allows a WinRT (Win8) app to call a local data portal running in full .NET


Here is the [version 4.5.600 change log](https://github.com/MarimerLLC/csla/issues?milestone=8&amp;page=1&amp;state=closed).

You can download the msi installer from the [release page](https://github.com/MarimerLLC/csla/releases/tag/v4.5.600), or better yet add references to the framework [via NuGet](http://www.nuget.org/packages?q=csla).

Version 4.5.600 includes support for iOS (via Xamarin) and for WinRT on Windows Phone 8.1 in the WinRT.Phone project. This also means you can use the new Universal solution/project type to build WinRT apps for Windows 8.1 and Windows Phone 8.1.

This prerelease also includes the new HttpProxy/Host and BrokeredProxy/Host data portal channels.

The Http data portal channel allows you to host the data portal server directly in ASP.NET MVC 4 or MVC 5 without the need for WCF. It relies only on the HttpClient library to invoke the server, so the client has no dependency on WCF - important for the new Windows Phone 8.1 programming model where WCF doesn't exist.

The Brokered data portal channel allows you to host the data portal server in .NET as a brokered assembly, thus available to a WinRT client app. This means you can build a WinRT app that makes data portal calls, where the "server-side" code is also running on the client device, but has access to full .NET. This will only work on Intel-based devices where full .NET assemblies can be deployed. It will only work with side-loaded apps, not apps from the Windows Store.
