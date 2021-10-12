---
title: Microsoft .NET and CSLA .NET version confusion
postDate: 2007-12-07T14:29:51.0996688-06:00
abstract: 
postStatus: publish
---
07 December 2007

I rather expected this - a bit of confusion around .NET versions and related CSLA .NET versions.

Microsoft started the whole thing by calling .NET 2.5 version 3.0. Oops, did I say that out loud? :)

But it is true. From a .NET programming perspective, 3.0 is purely additive over 2.0. Thus it is really hard to see why it is a major version.

*Especially* when .NET 3.5 has a much bigger impact on day-to-day use of .NET, but is just a point release... If anything, this should have been .NET 4.0, but it isn't and so now we're all royally stuck in the land of confusion.

Nothing to do but make the best of it.

I know several people and organizations who ignored .NET 3.0, but are now looking to move to .NET 3.5. Effectively "skipping" 3.0, though the reality is that their move to 3.5 is also a move to 3.0. Personally I think that's smart - they saved themselves a year of pain by not trying to use .NET 3.0 with the limited tools available, and can now move to 3.0/3.5 with Visual Studio 2008 - so they have decent tool support for the technology.

When it comes to CSLA .NET, here's my take on it:

- CSLA .NET 1.5.3 - latest version for .NET 1.x
- CSLA .NET 2.1.4 - effectively obsolete
- CSLA .NET 3.0.3 - latest version for .NET 2.0 *and* .NET 3.0
- CSLA .NET 3.5.0 - in-progress version supporting .NET 3.5


At this time I do not anticipate being able to make CSLA 3.5 work without .NET 3.5, primarily due to use of new compiler features as well as LINQ and features in .NET 2.0a and 3.0a (aka .NET 2.0 SP1 and 3.0 SP1).
