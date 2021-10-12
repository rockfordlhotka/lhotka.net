---
title: CSLA 4 version 4.3 release
postDate: 2012-03-04T15:29:03.6318045-06:00
abstract: 
postStatus: publish
---
04 March 2012

I am pleased to announce the release of CSLA 4 version 4.3. It is available from the [CSLA download page](http://www.lhotka.net/cslanet/download.aspx) and from [nuget](https://nuget.org/packages?q=CSLA).

This release adds support for Silverlight 5.


> *Silverlight 4 is still supported. The assemblies are in a Silverlight4.zip file in the bin folder created by the setup program in your Program Files folder or other install location.*


Other major enhancements include:

- New binary serialization scheme for MobileFormatter resulting in *substantially* smaller data flowing across the data portal from Silverlight and Windows Phone client applications. The ProjectTracker sample application has been updated to use this new scheme – look at the app server web.config and the SilverlightUI and WpUI app.xaml.cs files to see how the client and server configuration is handled.
- Numerous enhancements to the business rules subsystem. See the [change log](http://www.lhotka.net/Article.aspx?id=1c287e08-d428-4c27-b538-d588e3c55775) for more information.
- Bug fixes to address some specific data portal issues. See the [change log](http://www.lhotka.net/Article.aspx?id=1c287e08-d428-4c27-b538-d588e3c55775) for more information.
- CommandBase now supports managed properties.


With this version, CSLA 4 now supports the following platforms:

- Microsoft .NET 4
    - Windows Forms
    - ASP.NET Web Forms
    - ASP.NET asmx services
    - WPF
    - WCF services
    - ASP.NET MVC 3
- Silverlight 5
- Silverlight 4
- Windows Phone 7.5
- Mono
    - OS X
    - Linux
- Mono for Android


The source code also includes a version of CSLA 4 that builds for WinRT (Windows 8) Consumer Preview. This is largely untested, but does demonstrate that existing business classes (especially those built for 3- and 4-tier deployments in Silverlight) can be simply recompiled for use in WinRT applications. Consider this a preview of CSLA 4 version 4.5, coming later this year with support for .NET 4.5 and WinRT.
