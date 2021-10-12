---
title: CSLA 4 version 4.5 alpha available
postDate: 2012-06-07T23:19:34.9588281-05:00
abstract: 
postStatus: publish
---
07 June 2012

I have put an early version of CSLA 4 version 4.5 (version 4.5.1) online. This is a stable alpha release that supports:

- Microsoft .NET 4.5
- WinRT Metro style apps on Windows 8
- Silverlight 5


You can get it from the [CSLA download page](http://www.lhotka.net/cslanet/download.aspx).

This version doesn’t currently support Windows Phone, mono, or Android because all work is being done using Visual Studio 2012. We’ll reintroduce support for those platforms as everything gets supported on VS12.

- This 4.5 release has the same functionality as version 4.3.12, plus some functionality we’ve added only to 4.5. Most notably:
- The .NET and WinRT data portal now supports the new async/await keywords through methods like CreateAsync and SaveAsync
    var obj = Csla.DataPortal.FetchAsync&lt;CustomerEdit&gt;(id);
- The ViewModelBase class for WPF and WinRT now has an InitAsync method so you can await initialization of the viewmodel object
    var vm = await new MyViewModel().InitAsync();
- Enhancements to business rule processing


See the [4.5 change log](http://www.lhotka.net/Article.aspx?id=76e23c41-1f45-4c2e-9891-0f1e244dc679) for more detail.

Because this is an alpha release, you should expect more changes as we improve support for .NET 4.5 (most notably ASP.NET Web Forms, MVC, and Web API), and for WinRT/Metro.

At the same time, this should be a reasonably stable release, especially on .NET where the platform is also stable. It is also reasonably stable on WinRT/Metro, though there are more changes involved there so there could be more bugs.

Please direct feedback to the [CSLA forums](http://forums.lhotka.net/forums/5.aspx).
