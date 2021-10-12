---
title: Improving CSLA 4 MobileFormatter behavior
postDate: 2011-11-12T12:41:27.0450763-06:00
abstract: 
postStatus: publish
---
12 November 2011

One of the primary goals for CSLA 4 version 4.3 (the next version we’ll be creating) is to improve the performance of the MobileFormattter that is used for Silverlight and Windows Phone applications. This is made all the more important, because it will also be used in WinRT applications in the future.

Sergey (a CSLA dev team member, and Magenic colleague) has been doing some heavy research into this area, and we’d originally thought to do the changes as part of the 4.2 release. It turns out that doing a really great job of optimization will require some breaking changes – at least for people who aren’t using managed backing fields. So we are deferring the bigger changes until 4.3.

In the meantime, Sergey has blogged about [how to improve performance of MobileFormatter](http://dotnetspeak.com/index.php/2011/11/how-to-improve-performance-of-csla-for-silverlight/) in 3.8 and 4 (4.0, 4.1, or 4.2). These are changes you can make to your CSLA codebase now if you want some of the performance benefits without waiting for the “big change” that’ll come in 4.3.
