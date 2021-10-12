---
title: CSLA .NET 3.6.1 Released (for Windows and Silverlight)
postDate: 2009-02-05T13:40:25.9183552-06:00
abstract: 
postStatus: publish
---
05 February 2009

It has been a month and a half since the release of CSLA .NET 3.6, which was the first release of a major .NET development framework to include Silverlight support.[![csla_logo1_72](binary/WindowsLiveWriter/CSLA.N.1ReleasedforWindowsandSilverlight_BFD8/csla_logo1_72_thumb.png "csla_logo1_72")](binary/WindowsLiveWriter/CSLA.N.1ReleasedforWindowsandSilverlight_BFD8/csla_logo1_72_2.png)

Today I am releasing version 3.6.1 for Windows and for Silverlight. This point release addresses several bugs and issues with 3.6.0, and should include no breaking changes. I recommend that all 3.6 users upgrade to 3.6.1.

You can review the CSLA .NET for Windows [change log](http://www.lhotka.net/Article.aspx?id=3052f53d-9f2f-44e5-ab43-214fa515d823), and the CSLA .NET for Silverlight [change log](http://www.lhotka.net/Article.aspx?area=4&amp;id=4e991255-fcbe-414c-8e0b-d5022b753063) to get an overview of the fixes and changes.

Some enhancements of note on the Windows side include:

- The use of “\_forceInit” to trigger static field initialization is no longer required
- Add methods to the ObjectFactory base class to make it easier to build a DAL using ObjectFactory
- Allow resetting the proxy type used by the data portal, and allow setting the proxy type through code, to make it easier to change the data portal configuration at runtime


Some enhancements of note on the Silverlight side include:

- The use of “\_forceInit” to trigger static field initialization is no longer required if your PropertyInfo&lt;T&gt; fields are declared public in scope
- The data portal WcfProxy now has better support for various configuration and subclassing options
- MobileFormatter now supports the DateTimeOffset type


Though 3.6.1 includes these enhancements, the primary focus is on addressing a few bugs and issues that have been discovered in 3.6.0. Whether you need these enhancements or not, you will benefit from the bug fixes.



On a related note, I have refreshed the pre-release of 3.5.3, which includes some important bug fixes for the 3.5.2 version. If you are using 3.5.2, I strongly suggest you evaluate 3.5.3 to see if it addresses any issues you are facing. Version 3.5.3 is a “floating test release”, which means it is stable, but will continue to be a catch-all for reported bugs over the next few weeks. You should strongly consider using 3.5.3 if you are facing any of the bug fixes it contains.

As Microsoft rolls out .NET 3.5 SP1 via Windows Update, it is my intent to stop supporting the 3.5.x version, as all 3.5 users should be able to move to 3.6.x. That’ll get me down to dealing with just four versions:

1. 3.6.x for Windows
2. 3.6.x for Silverlight
3. 3.0.x C#
4. 3.0.x VB


I expect 3.5.3 to be the final release of the 3.5 code line, and I expect that’ll happen sometime in March.

Thank you for using CSLA .NET, see you on [the forum](http://forums.lhotka.net/)!
