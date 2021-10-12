---
title: ADO.NET Entity Framework, LINQ and CSLA .NET
postDate: 2007-02-07T12:08:20.2120496-06:00
abstract: More explicit discussion of the roles of ADO.NET EF, LINQ and CSLA .NET.
postStatus: publish
---
07 February 2007

I get a lot of questions about the new ADO.NET Entity Framework and LINQ and how these technologies interact with CSLA .NET. I've discussed this in a [few other blog posts](http://www.lhotka.net/weblog/SearchView.aspx?q=linq), but the question recently came up on the [CSLA .NET forum](http://forums.lhotka.net) and I thought I'd share my answer:

<font face="Times New Roman" color="#000000" size="3">They are totally compatible, but it is important to remember what they are for.</font>

<font face="Times New Roman" color="#000000" size="3">Both ADO.NET EF and LINQ work with <em>entity objects</em> - objects designed primarily as data containers. These technologies are all about making it an easy and intuitive process to get data into and out of databases (or other data stores) into entity objects, and then to reshape those entity objects in memory.</font>

<font face="Times New Roman" color="#000000" size="3">CSLA .NET is all about creating <em>business objects</em> - objects designed primarily around the responsibilities and behaviors defined by a business use case. It is all about making it easy to build use case-derived objects that have business logic, validaiton rules and authorization rules. Additionally, CSLA .NET helps create objects that support a rich range of UI supporting behaviors, such as data binding and n-level undo.</font>

<font face="Times New Roman" color="#000000" size="3">It is equally important to remember what these technologies are <em>not</em>.</font>

<font face="Times New Roman" color="#000000" size="3">ADO.NET EF and LINQ are not well-suited to creating a rich business layer. While it is technically possible to use them in this manner, it is already clear that the process will be very painful for anything but the most trivial of applications. This is because the resulting entity objects are data-centric, and don't easily match up to business use cases - at least not in any way that makes any embedded business logic maintainable or easily reusable.</font>

<font face="Times New Roman" color="#000000" size="3">CSLA .NET is not an object-relational mapping technology. I have very specifically avoided ORM concepts in the framework, in the hopes that someone (like Microsoft) would eventually provide an elegant and productive solution to the problem. Obviously solutions do exist today: raw ADO.NET, , the DAAB, nHibernate, Paul Wilson's ORM mapper, LLBLgen and more. Many people use these various technologies behind CSLA .NET, and that's awesome.</font>

<font face="Times New Roman" color="#000000" size="3">So looking forward, I see a bright future. One where the DataPortal_XYZ methods either directly make use of ADO.NET EF and LINQ, or call a data access layer (DAL) that makes use of those technologies to build and return entity objects.</font>

<font face="Times New Roman" color="#000000" size="3">Either way, you can envision this future where the DP_XYZ methods primarily interact with entity objects, deferring all the actual persistence work off to EF/LINQ code. If Microsoft lives up to the promise with EF and LINQ, this model should seriously reduce the complexity of data access, resulting in more developer productivity&nbsp;- giving us more time to focus on the important stuff: object-oriented design ;) .</font>
