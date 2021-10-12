---
title: DataAnnotations not in the client profile
postDate: 2009-11-06T15:41:13.361-06:00
abstract: 
postStatus: publish
---
06 November 2009

In Visual Studio 2010 and .NET 4.0 Microsoft is amping up the visibility of the “client profile” concept. In fact, when you install the 4.0 client profile on a machine, it doesn’t drag the rest of the framework to that client later – they just get the client profile. And when you create a WPF or Windows Forms project in VS10 you default to targeting the client profile.

That’s all good – great in fact!!

But I’ve fallen in love with the validation attribute concepts in System.ComponentModel.DataAnnotations.dll. These attributes are designed specifically to enable a UI framework author (or a business layer framework author – like me with CSLA .NET) to automatically create a rich user experience based on the attributes decorating business objects.

This concept was first fully realized in Silverlight 3 – a client technology – and is now fully supported in .NET 4.0 *full profile*. But it is a *client side technology*, and so should be in the client profile.

I’ve logged this issue on connect, and recommend you vote for this to be resolved:

https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=502807


