---
title: Side-loading on Windows 8
postDate: 2012-08-21T10:35:55.5873513-05:00
abstract: 
postStatus: publish
---
21 August 2012

Most of the work Magenic does for our customers centers around enterprise app development. That’s another way of saying ‘line of business’ or LOB apps in most cases.

Most enterprise and LOB apps will never be placed into the Windows Store for deployment. They’ll typically be deployed from corporate servers to the devices (tablets, ultrabooks, laptops, desktops) of employees. In the mobile world this is called “side-loading”, but that’s just jargon for deploying apps without using a public store.

The Wikipedia page describing the Win8 editions is highly misleading:

[http://en.wikipedia.org/wiki/Windows\_8\_editions](http://en.wikipedia.org/wiki/Windows_8_editions "http://en.wikipedia.org/wiki/Windows_8_editions")

If you look at the last item in the comparison grid, it appears that only Windows 8 Enterprise supports side-loading. That is entirely wrong.

The following two links provide important details:

- [Deploying Metro Apps to Businesses](http://blogs.msdn.com/b/windowsstore/archive/2012/04/25/deploying-metro-style-apps-to-businesses.aspx)
- [How to Add and Remove Apps](http://technet.microsoft.com/en-us/library/hh852635.aspx)


The process for Windows RT (ARM devices) seems to be more polished than for Intel devices, and that is rather strange. But still, Intel devices can be enabled to side-load apps via domain policy or a command line script.

**The important thing to understand is that you can side-load enterprise or LOB apps to *all editions of Windows 8*. **

As I’ve [said before](http://www.lhotka.net/weblog/Windows8TerminologyAndConcepts.aspx), if you want to write Windows apps that can run on any Win8 device, you should be targeting WinRT as your development platform.
