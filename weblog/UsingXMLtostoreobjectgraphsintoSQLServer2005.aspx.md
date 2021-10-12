---
title: Using XML to store object graphs into SQL Server 2005
postDate: 2007-07-31T09:15:00.231952-05:00
abstract: 
postStatus: publish
---
31 July 2007

Srinivas Surampalli, a fellow [Magenic](http://www.magenic.com) consultant, just wrote the following article:


> [Using XML with Stored Procedures Effectively in SQL Server 2005](http://dotnet.sys-con.com/read/406637.htm)


One common question that comes up relative to CSLA data access is how to efficiently save an object graph where there's a parent with children or even grandchildren.

The typical answer is to make an INSERT/UPDATE/DELETE call for the parent and each child. This article shows a different approach, where you could put the business object data into a DTO object graph, serialize that object graph into XML and make a single database call.

What surprised me, looking at the article's code, is that the SQL in the stored procedure is so straightforward.

As always, you should test different approaches to find the one that works best for your application, based on performance, maintainability and other requirements.
