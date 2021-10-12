---
title: More issues with ASP.NET object data binding
postDate: 2005-11-15T09:55:10.046-06:00
abstract: 
postStatus: publish
---
15 November 2005

The ADO Guy [expresses his frustration](http://adoguy.com/viewrant.aspx?id=1974) that the ObjectDataSource doesn't work with typed DataSets in ADO.NET 2.0. In an earlier post I [expressed my frustration](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=c3293240-88c8-4f03-b4e3-01cef6ed1304) about using it with business objects.

In the case of CSLA .NET 2.0 I'm writing my own CslaDataSource that understands how to work nicely with CSLA .NET business objects. In conferring with the ASP.NET team it seems like this is the best option. It turns out that writing a DataSource control isn't overly difficult - it is writing the designer support (for VS 2005) that is the hard part...
