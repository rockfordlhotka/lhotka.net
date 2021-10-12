---
title: .NET Rocks! show spurs UML discussion
postDate: 2004-06-08T10:16:04.6875-05:00
abstract: Rocky was recently interviewed on the .NET Rocks! Internet radio show, and UML came up in the discussion along with Microsoft's upcoming Whitehorse designers.
postStatus: publish
---
08 June 2004

My recent [.NET Rocks!](http://www.franklins.net/dotnetrocks) interview was fun and covered a lot of ground. One technology that we discussed was the Whitehorse designers - the SOA designer and Class Designer - that are slated for Visual Studio 2005. In fact, Brian Randell and I co-authored an article on these designers that will come out in the July issue of [MSDN Magazine](http://msdn.microsoft.com/msdnmag/).

Since the Class Designer is an extension of the UML static class diagram concept, the conversation looped briefly through a discussion of the value and history of UML. At least [one blog discussion](http://www.torqsoftware.com/2004/06/agile-uml.html)was spurred by this brief interlude.

I use UML on a regular basis, primarily in Visio. I use it as a design tool and for documentation. I don't use it for code-generation at all, because I have yet to find a UML tool that generates code I consider to be acceptable. I think UML is a decent high level modeling tool for software, and I strongly recommend that anyone doing object-oriented design or programming use UML to design and document their system. Having a decent OO diagram is totally comparable to having an ER diagram for your database. You shouldn't be caught without either one!

At the same time, I think UML has become rather dated. There are concepts in both Java and .NET that just can't be expressed in UML diagrams in a reasonable manner. For instance, component-level scoping (Friend in VB, internal in C#) just isn't there. Nor is the concept of a *property* as opposed to a *field*. Nor can you really express events or delegates.

If you are going to even try to do code-gen from a diagram, the diagram must include all the concepts of your platform/language. Otherwise you'll never be able to generate the kind of code that a programmer would actually write. In other words, you can use UML to provide abstract concept diagrams for .NET programs, but you can't use UML to express the *details* because UML simply doesn't have what it takes.

Recognizing this, Microsoft has created this new Class Designer tool for Visual Studio 2005. It is *very* comparable to a static class diagram. It uses the same symbology and notation as UML. However, it extends UML to include the concepts of field vs property, events, component-level scoping and more. In short, the Class Diagram tool allows us to create UML static class diagrams that *can* express all the details of a VB or C# program in .NET.

If you are familiar with UML static class diagrams and with .NET, learning the Class Designer notation will take you all of 10 seconds or less. Seriously - it is just UML with a handful of concepts we've all been wishing for over the past several years.

But the real benefit is the real-time code synchronization. The Class Designer is *in your project* and is directly generated from your code. It is not generated from meta-data, but instead is generated from your VB or C# (or J#) code directly. This means that changes to the diagram *are* changes to your code. Changes to your code *are* changes to the diagram. The two are totally linked, because the source for the diagram is the code.

This is not reverse-engineering like we have today with Visio or other tools, this is directly using the VB/C# code as the 'meta-data' for the diagram.

(To be fair, there is an XML file for the diagram as well. This file contains layout information about how you've positioned the graphical elements of the diagram, but it doesn't include anything about your types, methods, properties, fields, etc. - that all comes from the code.)

My only reservation about the Class Designer is that I've mostly moved beyond doing such simple code-gen. Since coming out with my [VB.NET and C# Business Objects](/ArticleIndex.aspx?area=CSLA%20.NET) books, I've really started to appreciate the power of code generators that generate complete business classes, including basic validation logic, data access logic and more. Readers of my books have created CodeSmith templates for my CSLA .NET framework, Kathleen Dollard wrote an XSL-based generator in her code-gen book and Magenic has a really powerful one we use when building software for our clients.

While the Class Designer is nice for simple situations, for enterprise development the reality is that you'll want to code-gen a lot more than the basic class skeleton...
