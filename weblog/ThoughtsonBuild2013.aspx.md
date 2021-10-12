---
title: Thoughts on Build 2013
postDate: 2013-07-01T17:14:12.570314-05:00
abstract: 
postStatus: publish
---
01 July 2013

After having a couple days to collect my thoughts regarding last week’s Build 2013 conference I want to share some of my observations.

First, I left Build happier with Microsoft than I’ve been for a couple years. Not necessarily due to any single thing or announcement, but rather because of the broader thematic reality that Microsoft really is listening (if perhaps grudgingly in some cases) to their customers. And the display of truly amazing, cool, and sexy laptops and tablets running Windows 8 was really something! I was almost literally drooling over some of the machines on display!

Now to summarize some of my thoughts.

The bad:

1. They didn’t add support for Silverlight in the WinRT browser (not that anyone really thought they would).
2. They didn’t fix (or even discuss) the nasty [business licensing cost issues around side-loading](http://www.lhotka.net/weblog/Windows8WinRTLicensingIdeas.aspx), meaning most businesses will still find WinRT unpalatable as a development target.


The good:

1. The changes in Windows 8.1 to provide some accommodations for people who are attached to the Start button are quite nice. To be honest, I was pretty skeptical that these changes were just silliness, but having used 8.1 Preview for a few days now I’m sold on my own positive emotional reaction to having the wallpaper the same on the desktop and start screen (though I’m still not booting to desktop, nor do I plan to do so).
2. The Windows 8.1 changes that bring the start screen experience more in line with Windows Phone are even nicer. The new item selection gesture (tap and hold) and the fact that new apps don’t automatically appear on the start screen (only on the “app apps” screen) are just like the phone, and make the system easier to deal with overall.
3. The updates to WinRT XAML are extremely welcome – especially around data binding – these are changes I’ll use in CSLA .NET right away.
4. The added WinRT API capabilities demonstrate Microsoft’s commitment to rapidly maturing what amounts to a Version 1 technology as rapidly as possible.
5. The fact that Azure had no big announcements, because they’ve been continually releasing their new stuff as it becomes available is wonderful! In fact, this whole “faster release cadence” concept from Windows, Azure, and Visual Studio is (imo) a welcome change, because it means that the overall .NET and Microsoft platform will be far more competitive by being more agile.
6. There was a serious emphasis on XAML, and most of the JavaScript content was web-focused, not WinRT-focused – and I think this is good because it reflects the reality of the Microsoft developer community. Most of us are .NET/XAML developers and if we’re going to shift to WinRT someday in the future it’ll be via .NET/XAML. For my part, if I’m forced to abandon .NET for JavaScript I’ll learn general JavaScript, not some Microsoft-specific variation or library – but if I see a viable future for .NET in the WinRT world, then I’ll continue to invest in .NET – and this conference was a *start* on Microsoft’s part toward rebuilding a little trust in the future of .NET.
7. The new 8” tablet form factor is way nicer than I’d expected. I had a Kindle Fire and ultimately gave it to my son because I already have an eInk Kindle and couldn’t see a good use for the Fire. But an 8” Win8 tablet is a whole different matter, because it runs the Kindle app *and it runs Office* and WinRT apps so it is immediately useful. The small screen means amazing battery life and light weight, and the ATOM processor means it runs Win32 and WinRT apps – I’m really enjoying this [new Acer device](http://www.engadget.com/2013/06/24/acer-iconia-w3-now-on-sale-in-the-us/)!


The neutral:

1. As I tweeted last week the one recurring bit of feedback I heard from people was disappointment in the lack of WPF announcements or content. I’m not overly concerned about that, because I view Windows Forms, Silverlight, and WPF as all being the same – they are all in maintenance mode and Microsoft is just keeping them running. The same unprecedented stability enjoyed by Windows Forms developers for the past 8 years is now the reality for WPF too. Sure, this might be a little boring to be on an unchanging platform, but the productivity is hard to beat!!
2. Related to the lack of WPF content I want to suggest a different interpretation. WinRT with .NET/XAML is (imo) the “future of WPF”. What we *really* need to see is WinRT XAML continuing to rapidly evolve such that it becomes a natural progression to move from WPF/Silverlight to WinRT at some point in the future. I am encouraged by what was presented at Build in terms of the evolution of WinRT XAML, and if that continues I think we’ll find that moving to WinRT will become pretty attractive at some future time.
3. There was some content on the use of WinRT to create business apps, and that content was welcome. If-and-when Microsoft does fix the side-loading licensing issues so WinRT becomes viable for business use it is nice to know that some serious thought has gone into design and development of business apps on the new platform.


In conclusion, the overall vibe at the conference was positive. Attendees were, from what I could see, enjoying the conference, the content, and the technology. Moreover, I think Microsoft has taken a first small step toward rebuilding their relationship with (what was once) the Microsoft developer community (not that Azure ever lost this rapport, but the Windows client sure did). If they continue to build and foster this rapport I think they can win back some confidence that there’s a future for .NET and/or Windows on the client.
