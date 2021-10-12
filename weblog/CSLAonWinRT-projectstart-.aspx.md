---
title: CSLA on WinRT (project start)
postDate: 2011-09-18T21:36:28.0486988-05:00
abstract: 
postStatus: publish
---
18 September 2011

A number of people have asked about the future of CSLA .NET on WinRT (and Windows 8 and Metro).

(fwiw, you can always check out the [CSLA roadmap](http://www.lhotka.net/cslanet/roadmap.aspx) to see what I’m planning)

The short answer is that (when Win8 comes out) I expect to have a CSLA 4 version 4.5 release that supports .NET 4.5, along with WinRT.

These are two different things.

**.NET 4.5** builds apps that run on the Win8 desktop, not in Metro. I imagine .NET 4.5 will also support Win7, but I don’t know for sure. I was able to build the existing CSLA 4 version 4.2 code in .NET 4.5 without change. But I do expect that some changes will be required to take advantage of .NET 4.5 features.

For example, ASP.NET Web Forms is getting a major facelift in 4.5, as is ASP.NET MVC. It is reasonable to expect that CSLA will need to accommodate those changes – though the bulk of the impact should be in the Csla.Web and Csla.Web.Mvc projects.

Whether there are any interesting changes to WPF or Windows Forms is, at this point, something I haven’t explored.

**WinRT **is closer to Silverlight than full .NET, but it isn’t Silverlight either. I spent a couple hours this evening starting the port of CSLA 4 version 4.2 to WinRT.

1. I started with the Csla.Silverlight project, because it is closest to what will work in WinRT
2. I added the DataAnnotations implementation from Csla.Wp, because WinRT doesn’t have DataAnnotations
3. WinRT is also missing *both*INotifyDataErrorInfo and IDataErrorInfo – so it isn’t clear how any validation errors can be reported to the UI from a business object (I hope they have some solution)
4. I still need to add the WCF data portal service reference to the Csla.WinRT project, but it appears that the data portal is essentially the same as in SL


What remains are a couple relatively big issues that require some research:

1. The BackgroundWorker component doesn’t exist in WinRT, and we’ll need to either rewrite it or switch everything to the new async/await model
2. The .NET Type type is quite different in WinRT, so a lot of MethodCaller code needs to be changed to use the new WinRT type system


The MethodCaller issue is, I suspect, just a matter of learning and using the new type system. But this reveals an interesting fact: anyone using System.Reflection in their code (even for simple things) is probably going to need to make changes to move to WinRT.

The BackgroundWorker issue is more interesting. At first glance it seems obvious that we’d want to move to the async/await model. And I would – except that this model doesn’t exist in .NET 4, Silverlight 4, Silverlight 5, WP7, or WP7.5.

Silverlight 5 and WP7.5 are the challenges here, because they’ll be widely used concurrently with .NET 4.5 and WinRT over a period of months or years.

1. If we *require* the use of async/await, then CSLA 4.5 could not support SL 5 or WP7.5 (this violates one of the key value statements of CSLA .NET)
2. If we use async/await in .NET/WinRT, then you can’t have compatible object code between .NET/WinRT and SL/WP (this violates one of the key value statements of CSLA .NET)
3. If we re-implement BackgroundWorker in WinRT, then CSLA and your business code is unaffected, but you won’t be able to use async/await when you interact with the async data portal or async business rules
4. If we *support* the use of async/await on .NET/WinRT, but also support BackgroundWorker then *you* get to choose whether to write cross-compatible code, or code that works on 4.5/WinRT only


Clearly options 1 and 2 won’t work. So we have to explore re-implementing BackgroundWorker in WinRT. Presumably we’ll use async/await *inside* our BackgroundWorker replacement, but we’ll keep the external interface consistent. I hope this is possible – I’m just thinking out loud at this point.

In the medium timeframe option 4 has to be the goal. In the *long run* I think it is safe to assume that some future version of SL and some future version of Windows Phone will support async/await. When all the then-current Microsoft platforms support the model we’ll drop BackgroundWorker entirely.

Regardless, I am quite pleased by just how far I was able to get in just a couple hours work. I have the Csla.WinRT project structure in place, and have narrowed down the problem areas to:

1. We need some validation error notification model to replace IDEI and INDEI
2. We need a BackgroundWorker replacement
3. We need a MethodCaller update


When you think about the breadth of scope of the CSLA 4 framework, I’m pretty amazed that we only have three problem areas to address for the core framework.

We’ll also need to create a Csla.Xaml.WinRT assembly with some UI helpers (that’s probably how we’ll solve the validation error issue for example). I haven’t explored how much of the existing Csla.Xaml concepts will carry forward – but I suspect Csla.Xaml.WinRT will be very much like the existing Csla.Xaml.Wp project.
