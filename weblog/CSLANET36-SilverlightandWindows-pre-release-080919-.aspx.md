---
title: CSLA .NET 3.6 (Silverlight and Windows) pre-release (080919)
postDate: 2008-09-19T22:30:05.7240624-05:00
abstract: 
postStatus: publish
---
19 September 2008

I have put a new pre-release of CSLA .NET for Windows and CSLA .NET for Silverlight (both version 3.6) online for download:

- [CSLA .NET for Windows](http://www.lhotka.net/cslanet/download.aspx)
- [CSLA .NET for Silverlight](http://www.lhotka.net/cslalight/download.aspx)


This is a pretty major update to the last pre-release, and I believe we're very near feature complete and are pretty stable at this point. I think the next release will be Beta 1 if we hold to the current plan.

Read the change logs to see what's new, and check out the list later in the post for highlights.

Check out the samples download for Silverlight, and also many of the subfolders in the Silveright test download. Combined, they provide a wealth of examples on how to use the *many* data portal configurations, the really cool UI components and the flexible authentication options.

Also, the ProjectTracker code for .NET is nearly final. I have about 1.5 chapters left on the 2008 book (first draft), which means only the WCF service interface is likely to change much at this point. The WPF and Web Forms interfaces got a lot of focus due to chapters covering them. Sadly Windows Forms has no chapter, and so it is lagging a bit (and it could use some help, because there are cool new WinForms controls too!!).

For CSLA .NET for Windows users, here's a quick overview of what 3.6 adds to 3.5.1:

- ObjectContextManager to manage Entity Framework contexts
- TransactionManager to manage ADO.NET transaction objects
- PropertyStatus control for WPF to provide visual cues for validation and authorization on bound properties
- ObjectStatus improvements for WPF to provide bindable properties for authorization (so you can enable/disable/alter your UI through XAML)
- BusyAnimation control for WPF that you can bind to the CslaDataProvider or business object IsBusy property to automatically show when some background task is running
- Async data portal for parity with Silverlight, not real useful in WPF with a data provider, but still kind of neat
- Async validation rules for parity with Silverlight (because any rule using the data portal is, by definition, async)
- MembershipIdentity class to make it *very* easy to authenticate against the ASP.NET membership provider from a smart client app, or web app (or Silverlight app)
- The data portal no longer requires your principal subclass BusinessPrincipalBase, allowing for more flexibility
- The data portal will invoke an "authorization provider" on every server call, allowing you to do high level authorization on each call
- ApplicationContext.User now just works in WPF - it detects WPF and works differently to deal with the WPF issues with principal objects
- WcfProxy for data portal is now *far* more configurable - using a subclass you can entirely alter the channel factory and WCF proxy objects
- DataMapper and UndoableBase now use dynamic method invocation instead of reflection to provide superior performance
- The data portal now supports the ObjectFactory attribute, providing an entirely new model for object persistence (different from the DataPortal\_XYZ model)


This is just the high level list - there are other small things changed in various places to make things easier. And for all that, there are only two breaking changes from 3.5.1!!

- Removed an ambiguous overload of the PropertyInfo&lt;T&gt; constructor
- Renamed GetProperty&lt;P,F&gt; to GetPropertyConvert&lt;P,F&gt; (and same for Set/Load/ReadProperty)


And just think - all this stuff is in the CSLA .NET for Silverlight version too, plus other Silverlight-specific features!
