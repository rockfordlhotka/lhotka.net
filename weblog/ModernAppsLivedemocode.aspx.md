---
title: Modern Apps Live! demo code
postDate: 2014-03-20T23:23:53.4435233-05:00
abstract: 
postStatus: publish
---
20 March 2014

The MyVote app is a complete modern app built by [Magenic](http://www.magenic.com) as a demo for Modern Apps Live! conferences.[![Logo](binary/WindowsLiveWriter/ModernAppsLivedemocode_59B/Logo_thumb.png "Logo")](binary/WindowsLiveWriter/ModernAppsLivedemocode_59B/Logo_2.png)

MyVote from Modern Apps Live! LV 2014 is available on the [MyVote releases](https://github.com/Magenic/MyVote/releases) page on GitHub.

The MyVote app is available for install

- [MyVote in the Windows Store for Windows 8](http://apps.microsoft.com/windows/en-us/app/78d8584a-2067-4b84-9ec3-e9a1eef44648)
- Apple app store for iOS devices


Although we’ve made the code available on GitHub, getting the app compiled and running is non-trivial of course, because this is a complete modern app with clients for

- WinRT
- iOS
- Android with Xamarin
- HTML 5/JavaScript single page app


and services that use

- Windows Azure SQL Server
- Windows Azure Mobile Services
- Windows Azure Web Sites
- Windows Azure Cloud Services


In GitHub the README.md file contains a list of places in the code where you’ll need to insert your own encryption and service keys. Beyond that you are largely on your own. If you are looking for a more detailed walkthrough of the implementation I can only suggest that you attend [Modern Apps Live!](http://www.modernappslive.com) in Orlando this fall.
