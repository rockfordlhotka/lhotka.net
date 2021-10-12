---
title: CSLA 4 mono platform porting update
postDate: 2011-03-09T17:16:38.6569719-06:00
abstract: 
postStatus: publish
---
09 March 2011

A few weeks ago I posted about my initial efforts to port CSLA 4 to MonoDroid. The idea being that business classes created for WP7 could be used on Android as well.

That inspired some people – which is awesome!

- Stuart Bale volunteered to help port CSLA 4 to MonoTouch, for iOS (iPhone/iPad).
- Jonny Bekkum (a long-time CSLA team member) volunteered to port CSLA 4 to mono – the open source implementation of .NET that runs on Linux, Windows, and other platforms.
- Kevin Ford volunteered to finish what I’d started by getting CSLA 4 ported to MonoDroid (in reality, he’d already started a parallel effort, and then merged his work into mine).


Initial code for all three projects has been checked into the svn code repository. Jonny has some test apps running in mono, so there’s some confidence in that code. Kevin has a small test app running in Android, so there’s some confidence there too (though it is earlier in the process). The MonoTouch port is the hardest of the three due to some limitations of MonoTouch, and we don’t know for sure that the current code works (though it does build in MonoDevelop).

My current plan is that CSLA 4 version 4.2 will be the release that includes support for mono, Android, and iOS – in addition to the existing support for .NET, Silverlight, and Windows Phone. That’ll be exciting!

If you are a developer on any of these three new targets, we’d appreciate any help in testing the code to see if it works, and to find solutions to anything that doesn’t work. Please post any issues or comments on the forum at http://forums.lhotka.net – thanks!
