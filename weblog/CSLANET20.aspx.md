---
title: CSLA .NET 2.0
postDate: 2005-08-09T22:26:18.75-05:00
abstract: I am working on it, don't worry :)
postStatus: publish
---
09 August 2005

Just to put questions to rest and reassure anyone who is concerned, I am actively working on CSLA .NET 2.0 and still intend to release 2nd editions of both the Expert VB and C# Business Objects books next spring - probably March or April.

A few people have asked if this is still the case, since my [web site post](http://www.lhotka.net/Articles.aspx?id=d9bcbe62-b5a3-4aba-aee5-453b67c73856) was a few months ago and I haven't updated it. But it turns out that the post remains pretty accurate and I really don't have much more to say :)

CSLA .NET 2.0 will use generics - primarily for collections. It will support the new databinding, primarily because the new databinding uses the same interfaces as today (yea!), with the exception that ASP.NET Web Forms databinding will require some UI helper classes because it sadly isn't as transparent as Windows Forms.

The big change will be that the DataPortal will support multiple transports (most likely including remoting, asmx and enterprise services). This sets the stage for transparent support of Indigo (now Windows Communication Foundation, WCF) when it comes out later. But it also allows choice between today's three primary RPC technologies in a very transparent manner.

The other big change from the .NET 1.x book versions is that CSLA .NET 2.0 and the books will be covering CSLA .NET version 1.5 plus. In other words, most of the functionality of 1.5 will roll forward, including the RuleManager, context transfer (for globalization), exception handling and so forth. The one big change here is that I don't intend to support in-place sorting of collections, instead opting for a *sortable view* approach more akin to the way the DataView works against a DataTable. This will be more powerful, simpler and (I think) faster.

I am also trying to preserve as much backward compatibility as possible while adding the new capabilities. For instance, I intend on keeping BusinessCollectionBase and adding a new BusinessListBase which uses generics. That said, there's no doubt that some changes to existing code will be required - I just don't know exactly what yet...

Of course my primary goal with the original books wasn't to promote CSLA .NET specifically as much as to demonstrate the process (and some specific solutions) of creating a framework in .NET to support distributed OO. That remains my goal, and I think the *lack* of earth-shattering change helps with this. A good framework shields business applications from changes in the underlying platform. In .NET 2.0 data binding changes, but we largely don't care. Generics get added, and we can use or ignore them without penalty. Indigo will show up and we will be shielded from its changes. ADO.NET 2.0 has some incompatibilities with 1.x and we are largely shielded from those changes. On the whole I am pretty pleased with how *little* change is actually required moving from .NET 1.x to 2.0.


