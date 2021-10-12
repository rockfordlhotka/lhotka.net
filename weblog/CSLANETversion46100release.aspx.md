---
title: CSLA .NET version 4.6.100 release
postDate: 2015-08-27T09:40:34.7040726-05:00
abstract: 
postStatus: publish
---
27 August 2015

*[![csla win8_full](binary/Windows-Live-Writer/CSLA-.NET-version-4.6.100-release_87D3/csla%20win8_full_thumb.png "csla win8_full")](binary/Windows-Live-Writer/CSLA-.NET-version-4.6.100-release_87D3/csla%20win8_full_2.png)This is a NuGet only release, we no longer supply an msi installer*

Release details on NuGet: https://github.com/MarimerLLC/csla/releases/tag/v4.6.100

Supported platforms:

- .NET 4, 4.5, 4.6
- Android (Xamarin)
- iOS (Xamarin)
- UWP (Windows 10)
- WinRT and WinRT Phone (Windows 8.1 and Phone 8.1)


Major changes:

- Updated to the final release of Windows 10 and the UWP SDK
- This and all future releases will be via NuGet only (no more msi installer)
- Removes support for Silverlight and Windows Phone 8 (Silverlight)
- Adds support for .NET 4.6
- Adds support for UWP (though today NuGet deploys the WinRT assemblies for UWP projects)
- Updates iOS and Android to the latest Xamarin versions
- Move nearly all code files into shared projects
- WinRT, iOS, Android, UWP all now use the exact same code files as .NET in every case - which is where a lot of the risk comes from because I may or may not have gotten all the compiler directives fixed up correctly.
- Add analyzers for Visual Studio 2015 and .NET 4.6 projects

