---
title: CSLA .NET 2.0.1 available
postDate: 2006-05-31T22:37:06.39-05:00
abstract: 
postStatus: publish
---
31 May 2006

CSLA .NET version 2.0.1 is now available for download at http://www.lhotka.net/cslanet/download.aspx. This is primarily a bug fix update to address various errata and issues that readers have found since the release of the original code. It does include a couple changes primarily geared toward simplification of code generation templates. You can see the [change log here](http://www.lhotka.net/Articles.aspx?id=9185ab08-1561-4a7f-8402-7542e679f870).

At a high level the changes (other than bug fixes) include:

- A new Initialize() method for use by code generation templates
- A new IEditableBusinessObject interface to allow polymorphic child objects in BusinessListBase-derived collections
- Better support for lazy loading of child collections (EditLevel property now visible from BusinessListBase, and null child object references now restored in UndoChanges)



