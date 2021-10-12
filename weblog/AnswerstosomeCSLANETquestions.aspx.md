---
title: Answers to some CSLA .NET questions
postDate: 2006-09-07T10:31:32.412-05:00
abstract: I get many questions about CSLA .NET, and whether it is a good fit for various projects and needs. Here are some good links and a recent Q&A about the framework.
postStatus: publish
---
07 September 2006

I get many questions about CSLA .NET, and whether it is a good fit for various projects and needs. Many times I put the answers on my web site - building a FAQ of sorts. Here are some links to good articles there, and a copy of a Q&A I recently did for a prospective [<font color="#669966">Magenic</font>](http://www.magenic.com/) client.


> [<font color="#669966">What is CSLA .NET?</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=e6d603c6-9a1a-4a9f-94af-dcbb2f0a75d0)
>
> [<font color="#669966">CSLA .NET technical requirements</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=98708f70-44fc-4d9a-b7dd-b1f6afb84e38)
>
> [<font color="#669966">Why move from CSLA .NET 1.x to 2.x?</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=bdd9dc84-ffe1-4307-823a-8c188e622a2a)
>
> [<font color="#669966">CSLA .NET Roadmap</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=6ae50dc6-7fa5-4568-ab53-05869f0b4dd4)
>
> [<font color="#669966">CSLA .NET 2.0 download page</font>](http://www.lhotka.net/cslanet/Download20.aspx) (which includes a summary of breaking changes)
>
> [<font color="#669966">CSLA .NET 2.0 change log</font>](http://www.lhotka.net/Article.aspx?id=1b043659-c5e2-4832-ae48-048ca281c038) (detailed list of changes from version 1.5)


Now for the recent Q&A:

**What are the drawbacks to using the CSLA?**

This question is too vague to be answered directly. No framework is perfect for all types of application, and CSLA .NET is no exception.

It is not particularly useful for creating non-interactive batch processing code - the .NET 3.0 WF technology is a better bet there. (though the activities in a WF can be created using CSLA, and that's a great model that the WF team really likes)

It is also not particularly useful for reporting. A good reporting tool like SQL Reporting Services is the right answer.

CSLA does require the use of good OO design. Where the DataSet works well (best?) when using VB3 style code-in-the-form architecture, CSLA really requires the application of OO design to build a true business layer. For some developers this can be a hurdle, because they are not used to doing OO design.

CSLA also has some [technical requirements](http://www.lhotka.net/Article.aspx?area=4&amp;id=98708f70-44fc-4d9a-b7dd-b1f6afb84e38). Depending on the transaction model you use, the DTC may be required. In *all*cases CSLA requires FullTrust code access security, so it can't be used in a partial trust environment (like on most commercially hosted web servers).

**Where do the CSLA and the Enterprise Library overlap?**

They don't. They are complimentary, see [<font color="#669966">this article</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=b6b197e1-5aa0-44dc-8548-f450de1a2913) for details.

**What is the roadmap for the CSLA?**

CSLA .NET is a framework for creating a reusable, object-oriented business layer for .NET applications. As such, it continues to evolve based on the evolution of the .NET platform. This means its roadmap generally follows Microsoft's lead, with some exceptions around enhancements to CSLA itself. At the moment the roadmap looks like this:

Version 2.0      - available now for .NET 2.0 and VS 2005

Version 2.1      - available Q3-06 with performance and feature enhancements

Version 3.0 (?) - available Q1-07 with full support for .NET 3.0 (WCF, WPF, WF)

Version 3.x      - available Q?-07 with support for .NET 3.5 (LINQ technologies)

Obviously the 3.x schedules are subject to change based on Microsoft's schedule.

(updated road map can be found [<font color="#669966">here</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=6ae50dc6-7fa5-4568-ab53-05869f0b4dd4))

**What is the model for integrating the CSLA with .NET 3.0\Windows Communication Foundation?**

I am working closely with the Connected Systems group in Redmond on this, and related technologies. Additionally, when I build CSLA .NET 2.0 I specifically designed it to allow for near-seamless integration of WCF.

Right now you can get an early version of a data portal channel for WCF [<font color="#669966">from here</font>](http://www.lhotka.net/Article.aspx?area=11&amp;id=0eec56bb-2a61-47c4-a9ca-f98371db1cad).

This allows existing applications using Remoting, Web Services or Enterprise Services to transition to WCF with NO CODE CHANGES. This is a very compelling feature of CSLA in my view.

Unfortunately that's not the whole story, and that's why a new version of CSLA will be required in the .NET 3.0 timeframe. CSLA uses the BinaryFormatter for some scenarios (n-level undo, cloning). To support the DataContract model, the NetDataContractSerializer is required instead, so the formatter needs to be pluggable. Again, I've been working with the PM who owns serialization, and this is not a major change to CSLA, and other than there being a new configuration switch this change should have NO IMPACT ON ANY APPLICATION CODE.

**How is the CSLA supported in production environments?**

CSLA is not a "product". I don't sell it, nor do I sell support for it. CSLA is part of my Expert VB/C# 2005 Business Objects books, and is covered under a very liberal, essentially open-source, license

[<font color="#669966">www.lhotka.net/cslanet/license.aspx</font>](http://www.lhotka.net/cslanet/license.aspx)

As such, support in a production environment is the responsibility of the organization using the framework.

**What is the typical model for extending\enhancing the CSLA so that one can take advantages of new versions and migrate the custom enhancements easily to the new CSLA runtime?**

CSLA is designed to include numerous extensibility points, allowing organizations to customize the behavior of key functionality without altering the core framework. This is most often handled through inheritance, where an organization inherits from a CSLA base class to create their own custom base class that extends or alters the core CSLA behavior. In other cases a provider model is used to allow organizations to replace pre-supplied providers with their own custom providers.

**What Application Service Provider and\or 24x7x365 customer references exist for CSLA implementations?**

[<font color="#669966">Magenic</font>](http://www.magenic.com/) can provide various case studies around their implementation of projects using CSLA .NET.

For my part, since I don't sell CSLA, I can't fund the process necessary to go through the legal hoops at most organizations to release their names as references. I do maintain [<font color="#669966">this list of organizations</font>](http://www.lhotka.net/Article.aspx?area=3&amp;id=a26b2727-f99d-485b-aa3e-a5466e534a2b) who use CSLA. I can say that the framework is used in a wide range of applications, from small to very large and mission critical.

Also, here are some unsolicited quotes from CSLA .NET users:


> "A day doesn't go by without me marveling at how elegant this CSLA is."
>
> "Rocky, I learned so much from your books. They had enlightened me on true OO practice, including David West's Object Thinking that you recommend. Thank you."
>
> "First, a huge thank you for an awesome business object framework. I've learned so much just by stepping through your code."
>
> "Having single handedly completed a rather major WinForms app, which has now been in operation for over a year at several sites, I can tell you that you absolutely cannot go wrong choosing CSLA."
>
> "I'd like to say that you did a great job on CSLA. I've found it very helpful in the creation of standardly developed and maintainable code among our teams."


**Are there any Visual Studio 2005 project templates available for using the CSLA within VS2005?**

CSLA includes a set of snippets and class templates for each object stereotype. Even more importantly, in my view, there are several [<font color="#669966">code-generation templates</font>](http://www.codeplex.com/Wiki/View.aspx?ProjectName=CSLAcontrib) available for CodeSmith and other code generators, and Kathleen Dollard's book on .NET code generation also includes a CSLA code generator. Additionally, Magenic has a very powerful and extensible code generator that we often use on CSLA projects.

While project and file templates offer some short-term productivity, properly implemented code generation provides increased productivity over the lifetime of the entire project and should be a requirement for any large initiative (CSLA based or not).
