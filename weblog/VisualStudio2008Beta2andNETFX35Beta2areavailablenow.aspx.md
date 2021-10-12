---
title: Visual Studio 2008 Beta 2 and .NET FX 3.5 Beta 2 are available now!
postDate: 2007-07-26T16:21:37.454-05:00
abstract: 
postStatus: publish
---
26 July 2007

Visual Studio 2008 Beta 2, along with Microsoft .NET 3.5 Beta 2, is available for download. Here's Soma's [official announcement](http://blogs.msdn.com/somasegar/archive/2007/07/26/announcing-the-release-of-visual-studio-2008-beta-2-net-fx-3-5-beta-2-and-silverlight-1-0-rc.aspx).

I find that downloading such huge sets of files requires a bit of help. My recommendation: [Free Download Manager](http://www.freedownloadmanager.org). This tool is awesome - indispensable in fact - if you do any downloads beyond small text files :) It does queued downloads, resumed downloads and throttling. Perhaps best of all, it does multi-threaded downloads, so it maximizes the use of your bandwidth when running at full throttle.

**Update: **Apparently there are some things you must do/fix before using VS 2008!! Read [ScottGu's blog post](http://weblogs.asp.net/scottgu/archive/2007/07/26/vs-2008-and-net-3-5-beta-2-released.aspx) about it!

**Update 2:** According to Juval Lowy, the svcutil.exe program in Beta 2 is broken. <strike>A workaround is to copy an older (Beta 1?) version of svcutil.exe over the top of the Beta 2 version.</strike>  *Instead, Justin Smith says that you need to run "sn.exe -Vr svcutil.exe" - apparently then you don't need to copy an older verison over the new one.*
