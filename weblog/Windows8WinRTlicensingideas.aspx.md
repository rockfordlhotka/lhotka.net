---
title: Windows 8 WinRT licensing ideas
postDate: 2013-03-05T14:33:53.7184045-06:00
abstract: 
postStatus: publish
---
05 March 2013

I’ve now done four posts where I summarize Microsoft’s side-loading licensing scheme in terms of just how it works, what it looks like from various business perspectives, and why I think they have designed this scheme to compete with the wrong target (iPad instead of HTML 5).

1. [Cost to enable side-loading on a Windows 8 device](http://www.lhotka.net/weblog/CostToEnableSideloadingOnAWindows8Device.aspx "Cost to enable side-loading on a Windows 8 device")
2. [Windows 8 LOB deployment ‘story’](http://www.lhotka.net/weblog/Windows8LOBDeploymentLsquostoryrsquo.aspx "Windows 8 LOB deployment ‘story’")
3. [Perspectives on WinRT app licensing](http://www.lhotka.net/weblog/PerspectivesOnWinRTAppLicensing.aspx "Perspectives on WinRT app licensing")
4. [Windows 8 WinRT sideloading update](http://www.lhotka.net/weblog/Windows8WinRTSideloadingUpdate.aspx "Windows 8 WinRT sideloading update")


If you work for a large enterprise with EA/SA agreements and an IT staff that manages all your domain-joined Windows 8 Enterprise workstations you can probably stop reading now. You are the one demographic that is well-covered by the existing licensing model.

If you are a small or medium business, or an enterprise (such as a franchise or co-op org) where you have lots of non-domain joined machines, machines that run Windows 8 Pro, Windows RT, or the lowly “Windows 8” basic edition, then read on.

After my first four posts I heard from community members and people inside Microsoft – “ok tough guy, you’ve said what’s wrong, now how would you do it right?” (to paraphrase of course ![Smile](binary/Windows-Live-Writer/Windows-8-WinRT-licensing-ideas_ABFF/wlEmoticon-smile_2.png) ).

My first reaction is that this isn’t my job. If Microsoft wants to make WinRT unpalatable for business developers so we all switch to cross-platform HTML 5/JavaScript (h5js) then who am I to stop them? Besides, don’t they have high-paid experts to figure this stuff out, and so why should I give my thoughts for free?

My second reaction is that from 2001-today I’ve had the pleasure of working with .NET, and these have been the most enjoyable years of my professional career. Although [TypeScript](http://typescriptlang.org/) appears to offer some reasonable wrapper around the horror that is JavaScript, I’d much prefer it if Microsoft *didn’t* destroy the idea of building WinRT apps with XAML/C#/VB.

So here are my thoughts – though please keep in mind that I’m not a licensing expert, nor did I stay at a Holiday Inn Express last night.

To be successful, WinRT licensing needs to address its real competitor: h5js and/or WPF+ClickOnce. If WinRT is going to levy an additional licensing cost above those technologies, then WinRT *must* have commensurate benefits to offset that cost.

What is the cost to deploy an h5js app? Effectively zero, because the app downloads from a <strike>web</strike> deployment server into a browser. The browsers are all free, there’s no per-workstation license to enable downloading HTML or JavaScript, so the cost is essentially zero.

What is the cost to deploy a WPF app with ClickOnce? Effectively zero, because the app downloads from a deployment server and is installed on the workstation through a standardized ClickOnce client process. No per-workstation license is required – as long as you have a legal copy of the OS, .NET (and thus ClickOne) are free.

I’ve already covered the costs of deploying WinRT apps in the current scheme in my previous blog posts. Those costs can easily add up to thousands or even millions of added dollars – just for the privilege of deploying your own app to your own workstations.

So does WinRT have benefits over h5js or WPF that make it work this added licensing cost? Probably not at this time. It is a version 1 technology and so is less mature than h5js or WPF. Unlike h5js it isn’t cross-platform, and unlike WPF it doesn’t have a simple pre-built deployment technology like ClickOnce. It does have two benefits: WinRT apps can run on ARM devices as well as Intel devices, and WinRT offers a superior model for building touch-enabled apps. I’ll let you decide if those benefits are worth thousands or millions of extra dollars.

Assuming we agree that WinRT *isn’t* good enough to justify the added licensing fees over its competition, the question becomes how to license WinRT side-loading in a competitive manner.

Microsoft has expressed the (imo) very valid concern that they don’t want to enable the free-for-all side-loading model of the Android world. And I agree – the last thing I want is for my kids to yet again be able to download random software from random locations that are infested with viruses and malware. I *really want control* over what gets into public stores. I *want* my software to be vetted when it comes from public locations.

At the same time, I absolutely don’t want added cost or overhead or complexity for apps coming from my corporate marketplaces. I’m in consulting, so the model must allow for Magenic to have a marketplace for our employees, and our consultants must also be able to leverage the marketplaces of our clients so we have access to their apps while we’re working for them.

Thus far I’ve accumulated some requirements:

1. No per-device licensing fees
2. One device must be able to access multiple marketplaces
3. Public marketplaces must be controlled (or perhaps there is just the one Microsoft Store)
4. People do work from home, where the “Windows 8” edition is most common, so it should support side-loading as well
5. InTune is a fine idea for deployment, but it shouldn’t be the only option – customized/tailored “marketplace” experiences should be possible


**No per-device fees**

Let’s start with this requirement. Microsoft doesn’t charge extra for us to use Windows for business, and it makes no sense as to why they think they can charge an extra tax for us to use WinRT for business. This includes discarding the $30/device fee as well as not *requiring* the InTune per-device/per-month fee.

If InTune has enough other value people will buy it, but h5js and ClickOnce don’t have a monthly fee, so WinRT needs a comparable model.

**Multiple marketplaces**

As I noted above, employees of a company like Magenic need access to the Magenic marketplace, and to the marketplace of the company(ies) where they are working as consultants. And one would hope we’d have access to the Microsoft Store as well! This implies a way for each device to access multiple “stores” or marketplaces.

**Public marketplaces**

I’m rather neutral about public marketplaces beyond the Microsoft Store. My only requirement here, is that if Microsoft did allow such a thing to occur then they should be able to revoke any public marketplace’s “license” or “key” if that vendor becomes a source (intentionally or unintentionally) for malware. The bar for any public marketplace should be as high as the Microsoft Store in that regard.

Or perhaps a better solution is to make public stores legally liable for malware. So it becomes possible for me to seek financial or legal recourse if a marketplace allows malware to slip through onto my device?

**Work from home**

It is patently absurd to think that I can go to Best Buy and purchase a lowly Windows RT tablet and it can side-load business apps, but the most common Windows 8 edition (Windows 8) can’t be used to run my business apps. I can’t envision any justification for this at all, so clearly this just needs to be fixed.

**No InTune requirement**

I understand the value of InTune – it does a lot of cool stuff, one of which is deployment. But not everyone wants all that other stuff, and making InTune the only real ClickOnce replacement makes WinRT uncompetitive. Again, h5js and ClickOnce have no monthly cost, and WinRT needs a zero cost option as well.

**The result**

As a result I think the answer is to license *deployment servers* not client devices.

And for public servers these licenses should be revokable so Microsoft can easily shut down rogue public marketplaces. I’ll leave the public marketplace concept alone for the rest of this discussion, as I’m much more interested in corporate marketplaces.

To make this work for a small business (think 2-500 employees) the cost of a deployment server license/key must be quite low. A 5 person company might spend 10’s or low 100’s of dollars by not beyond that. I can see how Microsoft might want the cost to scale somewhat, so you could envision deployment server licenses working against a “registered device” model. I honestly think Microsoft would be best served by *not* charging an extra fee, but if they feel they must find a new revenue source perhaps it could work like this:

- &lt;=100 devices $100
- &lt;=500 devices $500
- &lt;=1000 devices $1000


MSDN subscribers should get a &lt;=10 device license as part of their subscription, allowing for software development and testing.

EA/SA customers might get some deployment server license “for free” as part of their negotiated contract.

Interestingly, Windows Phone 8 already has a corporate marketplace concept built into the phone, where you can register your phone with a corporate marketplace. They (to my knowledge) only support one marketplace, but the core idea is there.

To make this work, a server admin must be able to revoke the registration of a client device (employee leaves, device stolen, etc.), and there should probably be a pre-built WinRT app users can run to register their device with a marketplace (perhaps based on access to an appropriate email domain – like WP8 again).

So a Magenic employee would run this WinRT device registration app and enter their magenic.com email address. Perhaps this causes the marketplace server to send an email to that address with a confirmation hyperlink. The user clicks that hyperlink to confirm and the marketplace completes registration of that device, making the apps in that marketplace available to the end user.

**Conclusion**

Again, I’m not a licensing expert. I’m simply looking at the competitive landscape and trying to figure out how to make WinRT financially competitive with h5js and WPF+ClickOnce. Assuming that WinRT has no incredible value proposition over its competitors (and I don’t see that it does) then it *must* provide a cost-comparable licensing/deployment model.

Given that h5js and WPF+ClickOnce have a zero licensing/deployment cost, the goal should be for WinRT apps to have a zero licensing/deployment cost.

At the same time, I surely don’t want *public* marketplaces to come into being without some *substantial* recourse and penalty for any such marketplace that becomes a vector for malware.

I think something along the lines of what I’ve proposed here can achieve these goals, and can make WinRT into a viable business development platform in the future. My guess is that Microsoft has a few months, perhaps 18 at most, to make this happen (or at least to lay out a clear roadmap) before business developers *really* start migrating away from Windows toward h5js in an effort to ensure their careers remain vibrant and healthy.
