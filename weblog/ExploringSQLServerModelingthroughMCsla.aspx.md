---
title: Exploring SQL Server Modeling through MCsla
postDate: 2010-03-04T11:06:23.691-06:00
abstract: 
postStatus: publish
---
04 March 2010

MCsla is a prototype that takes SQL Server Modeling (aka “Oslo” and “M”) and CSLA .NET, using them to create an end-to-end story. This story goes like this:

1. Developer creates a business database for business data
2. Developer writes concise DSL code
3. Developer “compiles” DSL code into the SQL Server Modeling repository
4. End user executes a runtime application, which dynamically creates a UI, business layer and data layer that uses the business database – all this based on the compiled DSL metadata stored in the repository


This saves the developer from a lot of work. In fact the developer writes perhaps 5% of the code they would have written to create the UI, business layer and data layer by hand.

See my discussion of the concepts and prototype in a three part video series:

[Exploring SQL Server Modeling through MCsla](http://msdn.microsoft.com/en-us/data/ff381673.aspx)

You can see the MCsla code in the CSLA .NET repository ([web view](http://www.lhotka.net/cslacvs/viewvc.cgi/mcsla/)) or grab it using any svn client from svn://svn.lhotka.net/csla/mcsla/tags/Video1001.
