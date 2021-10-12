---
title: ATI Radeon graphics driver fail
postDate: 2009-12-14T07:57:39.578-06:00
abstract: 
postStatus: publish
---
14 December 2009

I just got a new ATI AMD Radeon HD 5850 – nice looking high end graphics card. This replaces my previous nvidia card and is a pretty big upgrade.

Of course I’m running Windows 7 x64, probably the best operating system yet created. Seriously! :)

Unfortunately the driver and utility installer (Catalyst 9.11) from ATI won’t run on my machine. The InstallManagerApp.exe crashes almost immediately every time I try to run it. Windows 7 detects that it failed, but beyond that I’m not getting any details about why it failed…

I was able to use the Windows device manager to directly install the driver, so at least the card works. But without the Catalyst control panel, the card is always running at full speed, and therefore its fan is too – which is really loud and consumes tons of electricity.

What’s odd is that I recently put a different ATI card into another Win7 x64 box and Catalyst installed just fine.

I’m wondering if there’s some issue where Catalyst won’t install because I just uninstalled the nvidia card and its drivers?

In any case, I’m not real happy with ATI just at the moment…

**Update:** Thanks to helpful replies, here's the answer:

[http://forums.amd.com/game/messageview.cfm?catid=279&threadid=101103](http://forums.amd.com/game/messageview.cfm?catid=279&amp;threadid=101103)

In short, unpack the installer, then go to the \bin64 folder and type this:

**&gt;** ATISetup.exe -Install -Output screen
