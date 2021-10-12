---
title: CSLA .NET Version 4.6.400 released
postDate: 2016-06-01T10:33:18.9684501-05:00
abstract: 
postStatus: publish
---
01 June 2016

[![csla win8_full](binary/Open-Live-Writer/CSLA-.NET-Version-4.6.400-released_937A/csla%20win8_full_thumb.png "csla win8_full")](binary/Open-Live-Writer/CSLA-.NET-Version-4.6.400-released_937A/csla%20win8_full_2.png)This release of CSLA .NET is focused primarily on enhancing the existing Xamarin support. There is now a Csla.dll targeting PCL Profile111, which is the current profile for Xamarin.Forms projects and .NET Core.

There is also now a CSLA-Xamarin NuGet package that includes a Csla.Xaml.dll with support for Xamarin.Forms. This includes the same viewmodel base classes as the other XAML platforms, and an implementation of the `PropertyInfo` control tailored for use in Xamarin.Forms.

[@JasonBock](https://github.com/JasonBock) added even more analyzers for Visual Studio 2015 to help developers avoid common coding mistakes when building CSLA .NET business classes.

We now have support for the prerelease of Entity Framework 7.

The pt and pt-BR resources for Csla.dll have been updated. **Other languages need updates as well - please contribute if you are a native speaker!**

There is a new way to customize the server-side data portal by implementing an interceptor that is invoked via the new `DataPortalBroker`. ([#564](https://github.com/marimerllc/csla/issues/564))

Full details: https://github.com/MarimerLLC/csla/releases/tag/v4.6.400

The assemblies and packages are all available via [NuGet](http://www.nuget.org/packages?q=%22csla+.net%22).
