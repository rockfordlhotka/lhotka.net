---
title: Perspectives on WinRT app licensing
postDate: 2013-02-03T13:35:58.78-06:00
abstract: 
postStatus: publish
---
03 February 2013

*Note that this is one post in a series. Make sure to read them all. [This post](http://www.lhotka.net/weblog/Windows8WinRTSideloadingUpdate.aspx) provides an index to the set.*

In my previous blog post I discussed the [Windows 8 WinRT app licensing story for business apps](http://www.lhotka.net/weblog/Windows8LOBDeploymentLsquostoryrsquo.aspx). In that post I looked at the sideloading licensing model from a scenario-based perspective: large enterprise, medium, small, home user, developer/tester.

In this post I walk to explore a different way of thinking about the licensing. In fact, I think *this* is the core reason Microsoft’s licensing is so out of line with most of our expectations.

The core question: What is the primary competition Windows 8 faces?

Is it the iPad? Android tablets? Generally speaking BYOD.

Or is it WPF+ClickOnce, or HTML 5 and JavaScript? Generally speaking existing business app dev tools.

I’m increasingly confident that the Windows Division at Microsoft views the primary competitor as being BYOD. My evidence here is that Apple and the Android world *do* levy extra “taxes” for deployment of business apps to their devices. And they have built an ecosystem where additional infrastructure and tooling is required to manage mobile devices in an enterprise space. None of those things are free – hence everyone pays this “tax” to support BYOD in the enterprise.

Windows 8 appears to be following this model as well, by requiring extra licensing, infrastructure, and tools to support Windows devices in the enterprise. Basically Microsoft saw that people were willing to pay a BYOD tax on the other platforms and thought they’d be competitive by levying their own comparable tax for Windows 8. This makes pretty good business sense at one level, because it is a whole new revenue stream for Windows that hasn’t existed in the past.

The thing is, *most existing Microsoft developers* are looking at this new Windows 8 licensing/infrastructure and wondering what in the hell is going on???

We’ve spent the past 20 years or so building on the Microsoft platform from when it was a toy OS in the early 1990’s, to when it became an enterprise player in the 2000’s with .NET. Throughout all that time Microsoft’s licensing enabled us to easily build and deploy business apps on all Windows machines. No extra tax for business apps over consumer apps.

So now we’re looking at future app dev platform strategy. Where should we put our energy today so we’re best positioned into the future. And I’d suggest (coming from a Microsoft platform background) that we have three primary choices:

1. Continue with WPF+ClickOnce in the hopes that Microsoft either continues to support Win32/.NET far into the future
2. Switch to cross-platform HTML 5 and JavaScript to decouple from any specific client OS, including Windows
3. Focus on Windows Runtime (WinRT) because it is clearly the future of the Microsoft client platform, even though they want to increase the costs of deployment to their platform


Nobody I know of is considering switching to iOS as their primary enterprise client platform. Nor are they looking at Android in that light. Hence Microsoft (imo) is making a major mistake by creating a BYOD-based licensing scheme for Windows 8, thinking their competition is iOS/Android, because what they are *really* doing is providing a financial dis-incentive for us to move to WinRT, and by extension a financial incentive for us to either stay on WPF or move to cross-platform HTML5.

Personally, having built a bunch of stuff for WinRT, I *really, really, really* wish Microsoft would drop this financial dis-incentive. I very much enjoy building WinRT apps with .NET. It is an absolute joy to finally be able to build a .NET/XAML app that integrates so smoothly and deeply into the Windows platform. Given a chance, I’ll absolutely embrace a WinRT-based future for smart client business app development!!

But assuming Microsoft maintains the current licensing model I think WPF or HTML5 are the more likely smart client business app dev platforms.

WPF+ClickOnce is really nice of course. It offers a great deployment model without any new license/infrastructure tax. Working in .NET/XAML is a true joy (imo anyway). And I think this is a great stop-gap approach if you assume Microsoft *will* fix the WinRT licensing story to eliminate the added deployment tax. Or if you assume Microsoft will waver in their focus on WinRT and will return to building on Win32.

I very much doubt they’ll return to any focus on Win32. I think that platform is now pure legacy. By extension WPF is also pure legacy (along with Silverlight and Windows Forms). So I don’t hold out any hope on that front.

I do hold out hope that Microsoft will fix the WinRT licensing story. They just need to realize that the primary competitor is HTML 5, not iOS.

So let’s talk about HTML5. From a Microsoft developer perspective switching to HTML5 as a smart client platform means complete retooling. Throw away all you know about C#/VB, the .NET framework, BCL, etc. Start over with HTML, CSS, and JavaScript, plus myriad open source JavaScript libraries. There is no “single platform” for HTML5 like there is for .NET – the “platform” varies radically depending on which particular open source libraries are chosen for any specific app dev effort. And those libraries are much more fluid and less predictable than the .NET platform, so it is virtually impossible to predict how they’ll evolve over a 3-5 year period, much less a 10 year period (which is a preferable planning horizon for an enterprise app).

As a result, the real costs of building and maintaining apps in HTML5 are way higher than in something like .NET. On the other hand, you get the ‘benefit’ of always living on the bleeding edge. This might make it easier to retain top dev talent, even while making it harder to build and maintain major enterprise apps. Oh, and remember that top dev talent costs more, so odds are that even low-end dev shops will end up paying a lot more for their apps, because you just can’t expect what has been traditional mainstream dev resources to be real productive in such a dynamic environment.


> That’s not a slam on mainstream dev resources btw – that’s just reality. *Most* business developers much prefer to learn a toolset and platform and ply those skills for many years. They prefer to focus on the *business problems* more than on *platform problems*. As a business software manager I do want a coding cowboy or two, but I want the majority of my dev team to focus on the business more than on the technology. At the moment though, HTML5 doesn’t afford that option because the platform is too dynamic and volatile – so it is pretty unrealistic to think that mainstream dev resources will be nearly as productive as they were in .NET or Java or VB or C++/MFC.


All that said, the HTML5 platform is maturing. Dev tools (including from Microsoft) are improving rapidly. There’s the possibility that a subset of the myriad open source libraries will become a de facto standard for the platform as a whole. The next version of JavaScript looks like it will get some important language features for modern enterprise app dev. In other words, I really believe that if the enterprise app dev world does shift its focus to HTML 5 that the platform *will stabilize* over a few short years.

And in a sense Microsoft is “subsidizing” our move to HTML5 through the WinRT deployment tax. The money you *would* spend to deploy your WinRT business apps can be viewed as a type of savings you can apply to offset the increased cost of building and maintaining your HTML5 apps.

I strongly doubt that offset is enough to actually cover the increased costs of HTML5, at least in the short term. But again, if we all move to HTML5 I think the platform will stabilize over a few years, and as a result the costs of app dev and maintenance will go down over that time as well.

If you stop and think about this for just a second, it is pretty clear that this is a *horrific* outcome for Microsoft. To think that they had subsidized their entire “Microsoft developer community” to move to a cross-platform technology that eliminates the need for the Microsoft Windows client would be incredibly disheartening.

And this is why I think that, at some point in here, someone in a leadership position at Microsoft will realize the mistake they are making, and they’ll fix the WinRT licensing/deployment story so WinRT is at least as attractive for business apps as WPF+ClickOnce or HTML5.

Or they won’t come to that realization. In which case I strongly suspect Windows will become “just another BYOD OS” alongside iOS, Android, and ChromeBook. In that future the client device is a pure commodity play, because all devices will run all apps. The only way people will choose one device over another is by price and cosmetics – much like we choose automobiles today.

All automobiles do the same thing: get us from point A to point B. But we choose various brands for cosmetic reasons, or for price, or for status.

The thing is, it is hard to predict what such a *fundamental* change would do to Microsoft, Apple, or Google. Odds are it wouldn’t be ideal for Microsoft or Apple, because their offerings have higher costs – so they’d probably end up more like BMW and Cadillac, while most of us will run cheaper-but-still-perfectly-functional ChromeBook devices (the Ford/Chevy/Toyota equivalent).

On that note I’ll leave you (dear persistent reader) with one final thought.

Business moves slowly. Most organizations are just now moving to Windows 7, and won’t consider moving to Windows 8 (or any other alternative) for 2-4 years. As a result there’s *no reason for panic*. Keep building WPF+ClickOnce, or start a retooling strategy to HTML5. But remember that there’s no rush. Microsoft could *easily* fix the WinRT deployment tax problem in the next few months and your investment in WPF/Silverlight will translate pretty nicely to WinRT. Even your retooling costs for HTML5 wouldn’t be wasted given that you can build WinRT apps with JavaScript and WinJS as well as you can with .NET/XAML.

As a Microsoft evangelist I personally hope they make WinRT an attractive business app platform. That’d be the best possible outcome imo.

But if they don’t I’m pretty sure we’ll see a migration to HTML5 (well, really HTML6) over the next few short years, and that’ll be as exhilarating as when I switched from DEC/VAX programming to Windows ![Smile](binary/Windows-Live-Writer/Perspectives-on-WinRT-app-licensing_B537/wlEmoticon-smile_2.png)
