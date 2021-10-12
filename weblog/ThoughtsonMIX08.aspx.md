---
title: Thoughts on MIX 08
postDate: 2008-03-09T06:18:27.749-05:00
abstract: 
postStatus: publish
---
09 March 2008

I'm just back from the [MIX 08](http://visitmix.com/2008/) conference. This was the first conference I've attended in many years (around 10 I think) where I wasn't speaking or somehow working. I'd forgotten just how fun and inspiring it can be to simply attend sessions and network with people in the open areas. No wonder people come to conference!! :)

Not that it was all fun and games. I did have meetings with some key Microsoft people and Scott Hanselman interviewed me for an upcoming episode of [Hanselminutes](http://www.hanselminutes.com/) (discussing the various data access and ORM technologies and how they relate to CSLA .NET 3.5).

The Day 1 keynote was everything I'd hoped for.

Well, nearly. The first part of the keynote was Ray Ozzie trying to convey how Microsoft and the web got to where it is now. The goal was to show the vision they are pursuing now and into the future, but I thought the whole segment was rather flat.

But then [Scott Guthrie](http://weblogs.asp.net/scottgu/) came on stage and *that* was everything you could hope for. Scott is a great guy, and his dedication and openness seem unparalleled within Microsoft. I remember first meeting him when ASP.NET was being unveiled. At that time he seemed so young and enthusiastic, and he was basically just this kick-ass dev who'd created the core of something that ultimately changed the Microsoft world. Today he seems nearly as young and easily as enthusiastic, and he's overseeing most of the cool technologies that continue to change the Microsoft world. Awesome!

So ScottGu gets on stage and orchestrates a keynote that really illustrates the future of the web. [Silverlight](http://www.silverlight.net) (which makes me SOOoooo happy!), IE8, new data access technologies (like we needed more, but they are still cool!) and things like ASP.NET MVC and more.

As I expected, they released a whole lot of beta code. You can get a full list with links from [Tim Sneath's blog](http://blogs.msdn.com/tims/archive/2008/03/05/download-links-for-mix08-announcements.aspx). He also has links to some [getting started materials](http://blogs.msdn.com/tims/archive/2008/03/05/so-you-ve-installed-silverlight-2-beta-1-what-next.aspx).

The real reason for keynotes though, is to inspire. And this keynote didn't disappoint. The demos of Silverlight and related technologies were awesome! There was some funny and cute banter with the casting director from Circ del Sole as she demonstrated using a cool disconnected WPF app. There was a fellow RD, Scott Stanfield, showing integration of SeaDragon into Silveright so we can look (in exquisite detail) at the memorabilia owned by the Hard Rock Cafe company, some thought-provoking demos of Silverlight on mobile devices and more.

Now to be honest, I've never been a fan of the web development model. Having done terminal-based programming for many years before coming to Windows, I find it hard to get excited about returning to that ancient programming model. Well, a worse one actually, because at least the mainframe/minicomputer world had decent state management...

AJAX helps, but the browser makes for a pretty lame programming platform. It is more comparable perhaps to an Apple II or a Commodore 64 than to a modern environment, and that's before you get into the inconsistencies across browsers and that whole mess. Yuck!

Which is why Silverlight is so darn cool! Silverlight 2.0 is really a way to do smart client development with a true web deployment model. Much of the power of .NET and WPF/XAML, with the transparent deployment and cross-platform capabilities of the browser world. THIS is impressive stuff. To me Silverlight represents the real future of the web.

It should come as no surprise then, that I spent my time in Silverlight 2.0 sessions after the keynote. Sure, I've been working (on and off) with Silverlight 1.1/2.0 for the past several months, but it was a lot of fun to see presentations by great speakers like [Joe Stegman](http://blogs.msdn.com/jstegman/) (a Microsoft PM) and various other people.

One of the best sessions was on game development with Silverlight. I dabble in game development whenever I have spare time (not nearly as much as I'd like), and so the talk was interesting from that perspective. But many of the concepts and techniques they used in their games are things designers and developers will likely use in many other types of application. Background loading of assemblies and content while the app is running, and some clever animation techniques using pure XAML-based concepts (as opposed to some other animation techniques I saw that use custom controls written in C#/VB - which isn't bad, but it was fun to see the pure-XAML approaches).

Many people have asked about "CSLA Light", my planned version of [CSLA .NET](http://www.lhotka.net/cslanet) for Silverlight. Now that we have a Beta 1 of Silverlight I'll be working on a public release of CSLA Light, based on CSLA .NET 3.5. Microsoft has put a lot more functionality into Silverlight 2.0 than they'd originally planned - things like data binding, reflection and other key concepts are directly supported. This means that the majority of CSLA can be ported (with some work) into Silverlight. The data portal is the one big sticking point, and I'm sure that'll be the topic of future blog posts.

My goal is to support the CSLA .NET 3.5 syntax for property declaration and other coding constructs such that with little or no change you can take a business class from full CSLA and have it work in CSLA Light. This goal excludes the DataPortal\_XZY implementations - those will almost always be different, though if you plan ahead and use a DTO-based data access model even that code may be the same. Of course time will tell how closely I'll meet this goal - but given my work with pre-beta Silverlight 2.0 code I think it is pretty realistic.

Scott Guthrie indicated that Silverlight 2.0 Beta 1 has a non-commercial go-live license - right now. And that Beta 2 would be in Q2 (I'm guessing June) and would have a commercial go-live license, meaning it can be used for real work in any context.

The future of the web is Silverlight, and Beta 1 is the start of that future. 2008 is going to be a great year!
