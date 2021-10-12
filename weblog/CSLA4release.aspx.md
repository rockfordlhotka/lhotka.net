---
title: CSLA 4 release
postDate: 2010-07-23T10:05:02.2584559-05:00
abstract: 
postStatus: publish
---
23 July 2010

I am very happy to announce the release of CSLA 4, with support for .NET 4, Silverlight 4 and Visual Studio 2010.


> [Download CSLA 4 here](http://www.lhotka.net/cslanet/download.aspx)


This is a major release of the CSLA .NET framework, not only because of the support for the Visual Studio 2010 wave of technologies from Microsoft, but also because of significant changes to CSLA itself based on feedback and input from the vibrant [CSLA community](http://forums.lhotka.net/).

As always, CSLA .NET couldn’t exist as it does without the strong support I receive from Magenic. Thank you!

CSLA 4 is the result of a lot of effort on the part of a global development team:

- **Jonny Bekkum **is a C# software architect and developer at InMeta ASA in Norway. He has been developing large-scale enterprise applications on .NET and other platforms for more than 20 years, working in financial, retail, public and betting industries. Jonny has been using CSLA .NET since 2005.
- **Sergey Barskiy **is a principal consultant with Magenic. He is a Microsoft MVP. He has been in IT industry for 15 years. He has been using CSLA for 3+ years.
- Justin Chase is from Minnesota and currently works for Microsoft on the Expression team. He has been a CSLA contributor for more than 3 years and has a special interest in DSLs and code generation.
- **Blake Niemyjski **is a Software Development Engineer with CodeSmith Tools and a student at UW-Platteville. He has been a contributor to various open source projects over the past three years. In his spare time he enjoys flying, learning about new technologies and contributing back to the community.
- **Ricky Supit **has been developing software professionally for almost 20 years. He currently is focusing on web development technology including ASP.NET WebForm/MVC, Ajax, jQuery, and Silverlight. Ricky has been using Rocky Lhotka’s CSLA framework since Visual Basic 6.0. Ricky is currently working as software development manager for a fortune 500 health insurance company. He has a master degree in Computer Engineering.
- **Peran Borkett **lives with his family in South East England. He has worked as a software consultant in the City of London financial district for over 12 years. He has been using CSLA for several years and has recently started contributing to the framework.
- **Rockford Lhotka **is the creator of the popular CSLA .NET development framework, and is the author of numerous books, including Expert 2008 Business Objects. He is a Microsoft Regional Director and MVP, and a regular presenter at major conferences around the world. Rockford is the Principal Technology Evangelist for Magenic.


CSLA 4 includes significant new features. See the [change log](http://www.lhotka.net/Article.aspx?id=3852b8d8-e2f7-4277-b77e-bf375125b6c9) for a complete history of the changes from 3.8 to 4. Here are some important highlights:

- Requires Visual Studio 2010, .NET and (optionally) Silverlight 4
- New business and authorization rules system (details [here](http://www.lhotka.net/weblog/CSLA4BusinessRulesSubsystem.aspx), [here](http://www.lhotka.net/weblog/CSLA4BusinessRuleChaining.aspx) and [here](http://www.lhotka.net/weblog/CSLA4AuthorizationRules.aspx))
- Base list/collection types are now ObservableCollection for WPF; (BindingList implementations still exist for Windows Forms and some third party WPF controls)
- Support for MVVM in Silverlight and WPF
- Support for new Silverlight 4 data binding and validation features
- Support for ASP.NET MVC 2
- Allow an object to be bound to multiple bindingsource controls in Windows Forms
- Silverlight data portal is now as extensible as the .NET data portal
- Rework LINQ to CSLA to be easier to use
- .NET unit tests now run in mstest (though you may still be able to run them in nunit with some work)
- New solution and project structure to isolate UI technology support from the core framework
- Consolidated release for .NET and Silverlight


Since this is a major version change (from 3 to 4), there are numerous breaking changes, which are highlighted in the change log.

In terms of future activities:

- I am actively working on ebook and video content covering CSLA 4. Right now you can get special pre-release pricing on the CSLA 4 MVVM video series at http://store.lhotka.net. Watch for more ebook and video content on the store over the next few months.
- I am also actively working on CSLA 4 for Windows Phone 7, and I’ll have more information about this over the next few months.
- As always, http://www.lhotka.net/cslanet/Roadmap.aspx contains my plans for CSLA related work and content.


I hope you enjoy CSLA 4 and find it useful in your development efforts. I know the CSLA 4 development team has put a lot of work into this release, and we’re all excited to see how people make use of it to create cool applications.

Code well, have fun!
