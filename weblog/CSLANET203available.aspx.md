---
title: CSLA .NET 2.0.3 available
postDate: 2006-07-14T09:02:57.891-05:00
abstract: This is a bug fix update to address various errata and issues that readers have found since version 2.0.2 - with particular focus on the CslaDataSource control.
postStatus: publish
---
14 July 2006

CSLA .NET version 2.0.3 is now available for download at **www.lhotka.net/cslanet/download.aspx**. This is a bug fix update to address various errata and issues that readers have found since version 2.0.2.

Most notably, this version (hopefully) fixes the issues with CslaDataSource, where it would sometimes fail to find the business assembly. Please note that the type name is *case-sensitive* and typos are now the primary reason the type/assembly can't be found.

To give you some idea what's going on with CslaDataSource, here's the short story:

In CSLA .NET 2.0 (and in the books), I implemented CslaDataSource so it loaded the business assembly at design time (in VS 2005) to get the assembly's metadata. The metadata is needed for the web forms designer so the GridView and DetailsView controls can show the right columns/rows. And that worked, but had the problem that changes to the business assembly during development weren't picked up by CslaDataSource.

In 2.0.1 I altered CslaDataSource to load the business assembly in a temporary AppDomain. That allows me to unload the AppDomain and thus unload the assembly - so CslaDataSource can always reflect against the latest assembly. Which is a great idea, *except* that there's no supported (or even unsupported really) way to *find* the current business assembly. It turns out that VS 2005 puts the assemblies into a shadow directory, creating a new shadow directory each time you build your project or update an external assembly. To work around this, I am doing a sort of hack by inferring the shadow directory location and then finding the most recently created shadow directory (by date/time).

Now, in 2.0.3 I altered CslaDataSource yet again, to better infer the shadow directory location. My previous approach didn't handle having Csla.dll in the GAC, and failed at other (seemingly random) times as well. The new approach infers the shadow directory inside the primary VS 2005 AppDomain, and using the business assembly/type as the source location (rather than Csla.dll). This change appears to have fixed the random failures and should allow Csla.dll to be in the GAC. I doubt it allows the business assembly to be in the GAC, but (imo) that's not a good idea anyway.
