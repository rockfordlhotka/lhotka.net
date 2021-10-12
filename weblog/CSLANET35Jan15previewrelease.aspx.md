---
title: CSLA .NET 3.5 Jan 15 preview release
postDate: 2008-01-15T14:50:53.611504-06:00
abstract: 
postStatus: publish
---
15 January 2008

I have refreshed the CSLA .NET 3.5 download with much more recent code. (http://www.lhotka.net/cslanet/download.aspx)

The C# and VB versions of the framework and ProjectTracker are now very comparable. The only difference is that the VB framework doesn't have the LINQ extensions yet (though the C# version doesn't have the coolest parts yet either).

Some highlights:

1. All the new property/field/child management code is in both versions. The result is code reduction of ~35% per property and no more string literals for property names.
2. All the new child object code is in both versions. The result is no more plumbing code for child objects, "automatic" lazy loading support and consistent persistence for root and child objects.
3. Both versions have seriously enhanced type coercion that is used by the new property scheme and by DataMapper.
4. Both versions have much improved type casting for SmartDate, allowing much more flexible use of this type.
5. Check out the new ConnectionManager and ContextManager classes in Csla.Data for simplification of data access code with ADO.NET or LINQ.
6. ProjectTracker.Library now uses an external data access assembly, which was created using LINQ to SQL.


There are *many* other changes/enhancements/fixes - check out the [change log](http://www.lhotka.net/Article.aspx?area=4&amp;id=71994329-d218-4c02-a4d4-ce5ea4ac8d4b) for details. Or look at all the [green items in the wish list](http://www.lhotka.net/cslanet/WishList.aspx), because that's all in 3.5.

I am still planning to do a beta release around January 25, so this is probably the last preview release before the beta.

I'm still working on a number of issues, and have more testing to do in general, but this is getting reasonably close to the final 3.5 feature set.

If you have comments/questions/concerns, please voice them now! Once the beta starts I'll be doing bug fixes only.
