---
title: More on VS Orcas Beta 1 VPC and ASP.NET
postDate: 2007-05-11T10:01:33.407648-05:00
abstract: 
postStatus: publish
---
11 May 2007

Earlier [I blogged](http://www.lhotka.net/weblog/OrcasBeta1ASPNETNotEnabledByDefault.aspx) about the fact that the [Orcas Beta 1 VPC image](http://msdn2.microsoft.com/en-us/vstudio/aa700831.aspx) doesn't have ASP.NET set up with IIS, so you have to do that. Unfortunately there are a couple other issues I've discovered. Here's the full list:

1. IIS isn't configured for ASP.NET
2. Windows authentication isn't enabled for the default web site in IIS - blocking the use of VS debugging until you enable it
3. The default for a VS Orcas web site is to build for .NET 3.5. If you attempt to debug such a project (when it is set to run in IIS) you'll get an error dialog with a vague message about an authentication error. The reason for this is that ASP.NET only supports .NET 2.0. To resolve this, you must go into the web site's properties dialog and set its target .NET version to 2.0. You can still reference the 3.0 and 3.5 assemblies and use the new features, but VS must *build to .NET 2.0* or you can't debug in IIS.

But it isn't just the debugger - other features may not work properly either, possibly resulting in a "hang" when you try to access a page.


For those of you at my workshop at [VS Live](http://www.vslive.com) this past Sunday, this was why my web site wouldn't run properly in the VPC. Fortunately there is this workaround, but I hope Microsoft provides a more comprehensive solution in the release version, because it is quite confusing to have to set your build version back to 2.0 even though you are really building against 3.5...
