---
title: Application Architecture Guide 2.0
postDate: 2009-01-12T11:29:13.8938576-06:00
abstract: 
postStatus: publish
---
12 January 2009

![AppArch2.0_small.jpg](http://i3.codeplex.com/Project/Download/FileDownload.aspx?ProjectName=AppArchGuide&amp;DownloadId=52040)The Microsoft Patterns and Practices group has a new [Application Architecture Guide](http://www.codeplex.com/AppArchGuide) available.

Architecture, in my view, is primarily about restricting options.

Or to put it another way, it is about making a set of high level, often difficult, choices up front. The result of those choices is to restrict the options available for the design and construction of a system, because the choices place a set of constraints and restrictions around what is allowed.

When it comes to working in a platform like Microsoft .NET, architecture is *critical*. This is because the platform provides many ways to design and implement nearly anything you’d like to do. There are around 9 ways to talk to a database – from Microsoft, not counting the myriad 3rd party options. The number of ways to build web apps continues to grow, etc. The point I’m making is that if you just throw the entire .NET framework at a dev group you’ll get a largely random result that may or may not actually meet the short, medium and long-term needs of your business.

Developing an architecture first allows you to rationally evaluate the various options, discard those that don’t fit the business and application requirements and only allow use of those that do meet the needs.

An interesting side-effect of this process is that your developers may disagree. They may only see short-term issues, or purely technical concerns, and may not understand some of the medium/long term issues or broader business concerns. And that’s OK. You can either say “buck up and do what you are told”, or you can try to educate them on the business issues (recognizing that not all devs are particularly business-savvy). But in the end, you do need some level of buy-in from the devs or they’ll work against the architecture, often to the detriment of the overall system.

Another interesting side-effect of this process is that an ill-informed or disconnected architect might create an architecture that is really quite impractical. In other words, the devs are right to be up in arms. This can also lead to disaster. I’ve heard it said that architects shouldn’t code, or can’t code. If your application architect can’t code, they are in trouble, and your application probably is too. On the other hand, if they don’t know every nuance of the C# compiler, that’s probably good too! A good architect can’t afford to be that deep into any given tool, because they need more breadth than a hard-core coder can achieve.

Architects live in the intersection between business and technology.

As such they need to be able to code, and to have productive meetings with business stakeholders – often both in the same day. Worse, they need to have some understanding of all the technology options available from their platform – and the Microsoft platform is massive and complex.

Which brings me back to the Application Architecture Guide. This guide won’t solve all the challenges I’m discussing. But it is an *invaluable* tool in any .NET application architect’s arsenal. If you are, or would like to be, an architect or application designer, you really must read this book!
