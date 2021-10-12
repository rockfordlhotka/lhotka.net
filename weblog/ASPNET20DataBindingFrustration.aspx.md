---
title: ASP.NET 2.0 Data Binding Frustration
postDate: 2005-10-13T19:17:12.203-05:00
abstract: ASP.NET 2.0 has bi-directional data binding, but with a frustrating implementation
postStatus: publish
---
13 October 2005

<font face="Times New Roman" color="#000000" size="3">ASP.NET 2.0 has bi-directional data binding, which is a big step forward. This means you can bind the UI to a data source (DataTable, object, etc.) and not only display the data, but allow the user to do “in-place” editing that updates the data source when the page is posted back.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The end result is very cool, since it radically reduces the amount of code required for many common data-oriented web pages.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Unfortunately the data binding implementation isn’t very flexible when it comes to objects. The base assumption is that “objects” aren’t intelligent. In fact, the assumption is that you are binding to “data objects” – commonly known as Data Transfer Objects or DTOs. They have properties, but no logic.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In my case I’m working with CSLA .NET 2.0 objects – and they do have logic. Lots of it, validation, authorization and so forth. They are “real” objects in that they are behavior-based, not data-based. And this causes a bit of an issue.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">There are two key constraints that are problematic. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">First, ASP.NET insists on creating instances of your objects at will – using a default constructor. CSLA .NET follows a factory method model where objects are always created through a factory method, providing for more control, abstraction and flexibility in object design.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Second, when updating data (the user has edited existing data and clicked Update), ASP.NET creates an instance of your object, sets its properties and calls an Update method. CSLA .NET objects are aware of whether they are new or old – whether they contain a primary key value that matches a value in the database or not. This means that the object knows whether to do an INSERT or UPDATE automatically. But when a CSLA .NET object is created out of thin air it obviously thinks it is new – yet in the ASP.NET case the object is actually old, but has no way of knowing that.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The easiest way to overcome the first problem is to make business objects have a public default constructor. Then they play nicely with ASP.NET data binding. The drawback to this is that <i style="mso-bidi-font-style: normal">anyone</i> can then bypass the factory methods and incorrectly create the objects with the New keyword. That is very sad, since it means your object design can’t count on being created the correct way, and a developer consuming the object might use the New keyword rather than the factory method and really mess things up. Yet at present this is how I’m solving issue number one.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I am currently solving issue number two through an overloaded Save method in BusinessBase: Save(forceUpdate) where forceUpdate is a Boolean. Set it to True and the business object forces its IsNew flag to False, thus ensuring that an update operation occurs as desired. This solution works wonderfully for the web scenario, but again opens up the door to abuse in other settings. Yet again a consumer of the object could introduce bugs into their app by calling this overload when it isn’t appropriate.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The only way out of this mess that I can see is to create my own ASP.NET data control that understands how CSLA .NET objects work. I haven’t really researched that yet, so I don’t know how complex it is to write such a control. I did try to subclass the current Object control, but they don’t provide extensibility points like I need, so that doesn’t work. The only answer is probably to subclass the base data control class itself…</font>
