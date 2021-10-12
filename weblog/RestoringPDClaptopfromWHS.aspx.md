---
title: Restoring PDC laptop from WHS
postDate: 2010-03-21T00:15:40.4772557-05:00
abstract: 
postStatus: publish
---
21 March 2010

As I’ve said before, I love Windows Home Server. While it has many useful features, the core feature is automatic nightly image backups of my computers.

Of course a backup is only useful if you can do a restore, which I’ve done 2-3 times, and which has easily paid for WHS each time.

I recently got my PDC laptop (Acer Aspire 1420P) into a bad spot with some pre-release software. This happens, and I wasn’t worried because I have WHS backups. Just 60-90 minutes and I can have the machine back exactly the way it was at a previous point in time.

*Except* I ran into a snag. It turns out that the WHS restore CD from 2007 bluescreens when it tries to boot on the 1420P. OK, no problem, I downloaded the newer restore image from Microsoft, created a new bootable CD and got the restore app running.

But then the restore app didn’t find the LAN driver. Without a network driver you can’t restore – the network is how the restore app communicates with WHS. On the advice of friends I got the drivers off the latest WHS backup of my laptop [as described here](http://social.microsoft.com/forums/en-US/whssoftware/thread/430fbb73-5619-4466-a868-0134a8ece624/). Unfortunately they are 64 bit drivers, and the WHS restore app is a 32 bit app, so the drivers are useless.

Damn!

Some frantic web searching ensued, and finally I stumbled across an article that suggested the 1420P has much the same hardware as the 1410. I had nothing to lose, so I grabbed the Lan\_Atheros\_1.0.0.19\_Vistax64Vistax86\_A driver from the Acer support website – this is the LAN driver for the Aspire 1410 – and put it on a USB thumb drive where the WHS restore app could find it.

And that did the trick!! The WHS restore app found the driver, loaded it, and 48 minutes later my tablet was restored to a previous image and it is now working perfectly.
