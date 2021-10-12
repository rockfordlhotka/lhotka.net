---
title: CSLA .NET 3.0 Beta 1 available for download
postDate: 2007-05-21T20:00:02.9016912-05:00
abstract: 
postStatus: publish
---
21 May 2007

I have made CSLA .NET 3.0 Beta 1 available for download from the [CSLA download page](http://www.lhotka.net/cslanet/download.aspx).

The changes in CSLA .NET version 3.0 are primarily focused on adding support for .NET 3.0 features: specifically WCF and WPF. No extra work was required to allow business objects to invoke WF workflows or to be used from activities in a WF workflow. There are also some very important bug fixes and feature enhancements that most people will want even when not using .NET 3.0.

There are no major or intentional breaking changes from version 2.1.4 to version 3.0.

CSLA 3.0 *will work on .NET 2.0.* You do not need .NET 3.0 to use this version. Obviously the WCF/WPF/WF features are only available to you if you have .NET 3.0.

The WCF support comes in two forms: a data portal channel, and comprehensive support for the DataContract/DataMember attributes. The data portal support comes in the form of a new data portal proxy, which is functionally equivalent to the CSLA 2.0 channels. In other words, upgrading to WCF is entirely transparent. The DataContract support is an optional configuration switch you can set in app.config/web.config to tell CSLA to use the WCF serializer rather than the BinaryFormatter. This affects n-level undo and cloning. If you want to use DataContract instead of Serializable on your business classes you *must* use this config switch.

The WPF support comes as a set of controls. These controls provide support for validation (like the Windows Forms ErrorProvider), authorization and a couple other key features. There is also a CSLA data provider control, allowing the creation of codeless XAML forms in some cases (for read-only data).

In addition to the .NET 3.0 support, there are some other functional enhancements to various areas. Here are some highlights:

1. Validation RuleArgs are now more sophisticated, allowing for more expressive human-readable rule descriptions, and providing a better model for code generators when specifying arguments to be passed into a rule method.
2. A number of bugs in BusinessListBase related to data binding scenarios have been fixed. Event handling for other list classes has been standardized as well. You will likely find that data binding to grids is much more reliable in 3.0 than in 2.1.4.
3. SmartDate has some minor enhancements and bug fixes.
4. N-level undo now detects when edit levels are out of sync and throws an exception. This helps locate and debug problems where nested begin/cancel/apply calls are out of order. While this feature will most likely cause some short-term pain as you find these issues, the result is that your code will behave properly.


For the complete list of changes, see the [change log](http://www.lhotka.net/Article.aspx?area=4&amp;id=0c94aa82-b975-455b-a0c5-f4f7196a2408).

My plan is to leave this beta online for 2-3 weeks, followed by a second beta in mid-June and a release at the end of June. If you plan to move to CSLA .NET 3.0 within the next few months, please consider downloading and testing this beta. Let me know about any issues you find so I can resolve them for Beta 2.

Thank you!
