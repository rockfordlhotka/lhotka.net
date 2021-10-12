---
title: CSLA 4 version 4.2 alpha release
postDate: 2011-03-26T18:13:06.9164951-05:00
abstract: 
postStatus: publish
---
26 March 2011

There is now an alpha release of CSLA 4 version 4.2 available for download:

- [Download CSLA 4 version 4.2.0](http://www.lhotka.net/cslanet/download.aspx)


The big initiative for version 4.2 is to add support for the following platforms:

- Linux and OS X (via Mono)
- Android (via MonoDroid)
- iPhone and iPad (via MonoTouch)


This alpha release does not include binaries for these platforms, but does include code and sln files (for Visual Studio and/or MonoDevelop) you can use to build the source on each of the platforms.

At this point in time we have the following:

1. CSLA 4 builds and runs on mono in Windows and Linux.
    1. Core CSLA 4 functionality (Csla.dll) should be the same as on .NET 4.
    2. ASP.NET code using CSLA objects should work using Csla.Web.dll
    3. The Windows Forms support with Csla.Windows.dll is limited due to incompatibilities in data binding between real Windows Forms and the mono implementation of Windows Forms.
2. CSLA 4 builds and runs on Android. Use the MonoDroid tools in Visual Studio to build Csla.dll.
    1. You should find behaviors and features for Android identical to that provided for WP7.
    2. There is not currently an equivalent to Csla.Xaml.dll for Android.
    3. No testing has been done around the use of any remote data portal channel – only the local data portal has had any testing.
3. CSLA 4 builds and runs on iOS (iPhone/iPad). Use MonoDevelop on OS X to build Csla.dll.
    1. You should find behaviors and features for iOS identical to that provided for WP7.
    2. There is not currently an equivalent to Csla.Xaml.dll for iOS.
    3. No testing has been done around the use of any remote data portal channel – only the local data portal has had any testing.


Please remember, this is an alpha release, in the early stages of testing and stabilization. Any help you can provide in terms of testing and resolving issues is appreciated! Direct inquiries to http://forums.lhotka.net.

Other changes of note to existing .NET, SL, or WP7 users include:

- When an async rule completes, rules for affected properties are now also run
- BackgroundWorker from Csla.Threading is now available in WP7
- Some cleanup work was done around CslaIdentity – this shouldn’t be a breaking change, but the internals are now quite different
- Fix a bug in non-generic GetProperty where field wasn’t always set to the correct default value

