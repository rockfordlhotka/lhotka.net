---
title: Limitations of Portable Class Libraries
postDate: 2014-04-28T15:07:47.4499297-05:00
abstract: 
postStatus: publish
---
28 April 2014

As well all know, portable class libraries are pretty cool, but are restricted by the “lowest common denominator” effect.

For example, CSLA .NET supports the use of DataAnnotations along with the richer CSLA rules engine.

In trying to create one of the new “Universal PCL” assemblies to support WinRT on Win8 and WP8 I ran into the fact that WP8 doesn’t support DataAnnotations.

“No problem” I thought, “we already have our own implementation for WP8 Silverlight, for Android, and for iOS. I’ll just use that code.”

Which worked insofar as that I have a Universal PCL Csla.dll that builds.

But it doesn’t work because I can’t actually use that Csla.dll from WinRT on Win8 because *that* WinRT already has DataAnnotations and so there are type collisions.

As a result it isn’t clear to me that I can actually create a Universal PCL for CSLA – at least not one that supports DataAnnotations across all platforms like I’m able to do if I create one assembly per target platform (like I’ve been doing since 2007 with Silverlight 2).

I guess this makes sense. The guidance around creating a PCL is that you have code that is simple enough that it doesn’t include any platform-specific implementations that would be solved easily using #if directives. The internal implementation of some parts of CSLA is far from simple, and we do use #if directives to optimize for and/or leverage features of each of the 9 platforms currently supported by CSLA (yes, we really provide business code portability across NINE different platforms).

My personal feeling is that I’d rather support all 9 platforms as efficiently as possible, rather than compromise one or more of them just to use a fancy and optional new concept like the Universal PCL.

(of course if Microsoft and Xamarin add DataAnnotations to Windows Phone 8.1, Android, and iOS then I wouldn’t need to implement it in CSLA and that would also solve this problem – so maybe someday :) )
