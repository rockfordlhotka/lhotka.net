---
title: WPF vs Silverlight, really?
postDate: 2010-11-09T10:06:24.3108135-06:00
abstract: 
postStatus: publish
---
09 November 2010

Over the past few months there’s been this ongoing buzz about whether WPF is dead, or whether Silverlight is really mature – in short, people trying to figure out whether to use WPF or Silverlight or both.

Having worked with WPF since it came out, and with Silverlight 2.0 and higher since before it came out, I thought I’d share my thoughts.

This post flows from my experiences with CSLA .NET, [UnitDriven](http://unitdriven.codeplex.com) and [Bxf](http://bxf.codeplex.com) – three frameworks I’ve created or been directly involved with, that run on WPF (.NET), Silverlight and now Windows Phone 7 (WP7). With CSLA in particular, I’ve been maintaining this one codebase on .NET since 2001, and to my knowledge it was the first major framework ported to Silverlight from .NET. Also, as I write about this, I’m thinking about how I build XAML-based apps, using the MVVM pattern as discussed in the [CSLA 4 MVVM video series](http://store.lhotka.net/) and some of my previous blog posts.

The way I use SL and WPF there is no meaningful difference between them. My MVVM demos, for example, are mostly the same across WPF, SL and even WP7.

The business layer, created with CSLA 4, is typically identical across all three platforms. That’s one of the big benefits of CSLA 4, in that you can write your business, validation and authorization rules once and use them across multiple interface technologies. And with the data portal managing any interactions with the application server, you are shielded from any complexity or differences you’d normally encounter there as well.

The way I use MVVM, with a strong focus on having zero code-behind any XAML, means that nearly all interface control logic (any actual code in the presentation layer) is also reused. Any presentation layer code is either in the viewmodel, in value converters, in attached properties or custom controls. This reuse isn’t always 100%, especially when you get to WP7, because the tiny phone screen often forces a different user workflow than if you have a full-size screen like in WPF or SL. But between WPF and SL, the viewmodel code is typically the same, as is most value converter and attached property code. Some custom controls may be different – again especially on the phone.

This commonality of viewmodel code is thanks to the use of Bxf. But any decent MVVM framework will offer the same kind of abstractions, so your application code is never directly interacting with the UI shell or any platform-specific constructs or types.

With WPF and SL there are places of direct difference however, depending on how you structure your user experience.

- WPF doesn't have a URL based navigation scheme or a navigation framework, so you have to come up with your own UI framework to manage any sort of navigation model. I usually do this by having exactly one Window, and that hosts all my content in the form of UserControl objects, but you could use many Window objects.
- SL does have an *optional* URL based navigation scheme and framework, which is nice - makes things simpler. However, you can use the same "one Window that hosts UserControl objects" model just like WPF (hence my samples are the same). What you can't do is have a lot of Window objects (which to me is no loss, since the multiple SDI interface went out of style in 1997).
- WP7 also has a URL based navigation scheme and framework. I still use the hosted UserControl idea too, and that makes a lot of the code common with SL and WPF.


I think the thing to understand, is that while SL runs in the browser, it is a smart client technology. It is far more like WPF than like HTML. In fact it is virtually identical to WPF in most ways that matter for a business app.

And the key to my success in this area, is that all my business “forms” or “pages” are always a subclass of UserControl. So every bit of meaningful UI content (forms/pages) are UserControl objects that can be hosted by the UI shell. This means that I can usually change out the shell, or even have different shell styles (URL navigation vs Outlook-style navigation for example) and this has no effect on the actual business UI elements. Yes, the shell code may be different, but the business code is unchanged.

This is one powerful technique that makes it quite realistic to create your app in Silverlight, even using the navigation framework, and then port it to WPF if you need to in the future. You might have to write some new WPF shell code, but your UserControl XAML, your viewmodels, your business domain objects, your data access code and your database remain unchanged.

Beyond UI and navigation differences, there are some technical differences between WPF and SL, including:

- Some minor, niggling differences in XAML - this is the sort of thing I personally want fixed now that the WPF and SL product teams have merged - this niggling differences are stupid and are nothing but an annoyance – why is the binding Mode default different between WPF and SL (for example)??
- SL *requires* that all server interactions be async, WPF allows sync or async - I tend to use async in both places, because the user experience is so superior with async, I can't figure out why I'd want to punish my end users just because they are using WPF
- SL has the navigation framework, WPF doesn't
- WPF has an application model that includes navigation, but it is hopelessly broken - it tried to emulate the worst features of the web without any of the benefits - to me this is the "ActiveX Documents" of WPF
- WPF apps can use all of .NET, SL uses a subset - but the SL subset is everything I've needed to build typical business apps
- WPF apps can interact with the full client workstation hardware (odd peripherals, the full hard drive, etc)
- WPF apps are (typically) deployed via ClickOnce, SL apps are deployed transparently via the browser - so WPF is slightly more "in your face" for your users, but the difference should be pretty incidental
- WPF apps can tap into all of DirectX, though SL now has hardware acceleration for some graphics scenarios too - so this difference is probably less meaningful for most business apps than for games
- SL doesn't have the complexity of the legacy "crap" that comes with WPF (DataSet, IBindingList, etc) so it is a simpler, easier and more consistent programming environment
- SL runs on Windows, in the browser, on the Mac, in the browser on the Mac, and in WP7; WPF of course runs only on Windows


Again however, I come back to the same thing - I always use as little of any platform/technology as necessary to get the job done. SL is a subset, so if I can get the job done with SL then that's the best thing to do (I can always upsize to WPF later if necessary). If I can't get the job done with SL, I'll use WPF.

In my mind it is a superset/subset decision - always default to the subset that meets your needs.

As long as you understand both technologies, you can architect your UI so transitioning from SL to WPF is relatively easy (the other way isn't always so easy - because your WPF code might use superset technologies).

In conclusion, my recommendation has been (since SL3 at least) to design your app for SL, and fall back to WPF only if SL can’t meet your needs. The most common scenarios for business apps to fall back to WPF are:

- Your app is only occasionally connected, and is mostly offline, so you use a client-side database like SQL Express or SQL CE
- Your app needs to interact with client-side peripherals
- Your app needs full access to the client-side hard drive


I don’t think this is a “WPF vs SL” thing at all. I think it is a sliding scale, where you default to SL, and slide up to WPF if necessary. All the angst is unnecessary.
