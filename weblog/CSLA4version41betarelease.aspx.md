---
title: CSLA 4 version 4.1 beta release
postDate: 2010-10-22T14:35:18.1731553-05:00
abstract: 
postStatus: publish
---
22 October 2010

I am pleased to announce the first beta release of CSLA 4 version 4.1 with support for Windows Phone 7, and continuing support for .NET 4 and Silverlight 4.

[Download CSLA 4 version 4.1.0 here](http://www.lhotka.net/cslanet/download.aspx)

With this release, it is now possible to write a single business layer composed of business domain objects that run unchanged on a WP7 device, in Silverlight, on a Windows client, on Windows Server and on Windows Azure.

The samples download includes Samples\Net\cs\SimpleNTier, which does implement the following interfaces over one common business layer:

- Windows Phone
- WPF
- Silverlight
- ASP.NET MVC


Of course this is just the first beta release, so there’s more work to be done. At the same time, we have completed the vast majority of the effort, and it is quite possible to build WP7 applications using this beta.

As with all CSLA releases, this one does include some bug fixes and enhancements to other parts of the framework. Please see the [change log](http://www.lhotka.net/Article.aspx?id=9aad2f99-86eb-453b-a760-6303c3b27552) for a list of all changes. Enhancement highlights include:

- Add ability to get a consolidated list of broken rules for an object graph
- New BackgroundWorker component that automatically initializes background threads with the current principal and culture from the UI thread
- TriggerAction provides better debugging information, following the lead of many Microsoft XAML controls
- and much more…


In related news, [UnitDriven](http://unitdriven.codeplex.com) has also been updated to support WP7, and provides a pretty comprehensive unit test runner and framework for WP7 code. CSLA uses UnitDriven for its automated testing, but UnitDriven can be used for any application on .NET, Silverlight or WP7.

Similarly, [Bxf](http://bxf.codeplex.com) (Basic XAML Framework) has been updated to support WP7, thereby providing a common MVVM framework for WPF, Silverlight and WP7 UI development efforts. Some CSLA sample apps use Bxf, but Bxf can be used for any application, including those that don’t involve CSLA at all.
