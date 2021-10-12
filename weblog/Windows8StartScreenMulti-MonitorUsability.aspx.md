---
title: Windows 8, Start Screen, Multi-Monitor Usability
postDate: 2012-04-06T10:50:13.2637656-05:00
abstract: 
postStatus: publish
---
06 April 2012

I've been watching a number of discussion threads regarding the usability of Windows 8, especially regarding the start screen, Desktop application usage, and multi-monitor scenarios.

All I can say is don’t knock it until you try it.

I’ve been running Win8 on my tablet and laptop for a few weeks now. The work I do on my laptop is often multi-monitor, and is real work.

There are three themes I’d like to address, based on my full-time usage experience thus far.

First, some people feel that Microsoft is making a mistake by having WinRT (Metro style) and Desktop apps run on the same machine at the same time. I vehemently disagree. I *absolutely* want one machine that I can use as a tablet on the plane, and as a real computer when I get to my destination. My tablet does this (Samsung from //build/) for almost everything, except when I’m doing distributed computing demos and need my full laptop to run virtual machines (because my laptop has tons of memory and an i7, vs the tablet with less memory and an i5).

I love the fact that I have WinRT apps, which are far superior to most web sites, for consuming news, weather, etc. And I love the fact that the same machine, plugged into a small portable dock, has a keyboard, mouse, second monitor, and can run Visual Studio just fine!

Second, there’s this idea floating around that the Win7 start menu is superior to the new Win8 start screen. That doesn’t hold true for me. Let me explain why.

When I read the Microsoft blog post about the Win7 telemetry data they used to design the start screen, they were describing me. When I use Win7 I pin my common apps and web sites to the start bar, and to run any other apps I press the Windows key and type part of the application name, then press enter. Almost never do I actually use the start menu to browse for apps.

In Win8 (keyboard/mouse – desktop/laptop computer) I pin my common desktop apps to the start bar, and my WinRT apps to the first page or two of the start screen. And I still press the Windows key and type the first part of the application name to run other applications. In other words, THERE IS NO DIFFERENCE between Win7 and Win8 from my perspective – other than that the live tiles from news/weather/stocks/etc. make the start screen a useful dashboard – so it is BETTER than Win7.

(as an aside, I do have some Desktop apps on my start page tiles too – but I find that I rarely use those tiles, preferring instead to tap the Desktop tile and then launch from the start bar – a personal quirk I suppose)

Third, the multi-monitor problems aren’t as bad as they are being portrayed. But the story isn’t good either, and I truly hope it improves over the next few months.

If you are doing “real work” today, you are probably spending 90% of your time (or more) in desktop mode. And if you’ve pinned your common apps to the start bar (like Win7, and I have done this) then you’ll probably never leave desktop mode. And in this case, multi-monitor works just like Win7, but slightly better because the start bar works better in Win8 (or at least it has new options I find useful).

Where the multi-monitor falls down is if you are using a mix of WinRT apps and Desktop applications at the same time.

WinRT only runs on the primary monitor, and that’s just lame. It completely prevents the use of WinRT for many business scenarios where multi-monitor is critical. I honestly don’t expect this to get fixed in WinRT v1, but I hope we don’t have to wait for Windows 9 (2014?) for this to be solved, because it is a major blocker for WinRT development in the real world.

Between the Dev and Consumer previews, they did change the way WinRT apps use the primary monitor. At least now in the Consumer preview it is possible to keep a WinRT app running on the primary monitor while using a Desktop app on other monitors. I do find though, that it is too easy for some errant Desktop app to use the primary monitor, thus making the WinRT app disappear – and this is frustrating.

Sadly it is not possible to keep the start page visible while using a Desktop app on a secondary monitor – reducing its otherwise high value as a dashboard L

To summarize the multi-monitor scenario: if you are a Desktop app user, Win8 is as good or better than Win7, because you’ll only see the start screen when you press the Windows key to launch some non-pinned app. If you are a WinRT user multi-monitor is useless. If you are a hybrid user (like me) the experience is workable, but unpredictable and frustrating.

Clearly Microsoft needs to do more work in this area.

In final summary, don’t knock it until you try it full-time on real machines. The experience overall is quite good, and I VERY much like having WinRT apps that I can use on my main computer instead of using web pages with their inferior usability and aesthetics. Given that most of my main laptop usage is in Visual Studio, Word, and PowerPoint, I find the experience with multi-monitor to be adequate, and Win8 is just as productive for those scenarios as Win7.
