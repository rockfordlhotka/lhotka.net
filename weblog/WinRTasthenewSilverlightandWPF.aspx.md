---
title: WinRT as the new Silverlight and WPF
postDate: 2013-07-09T11:58:43.8876905-05:00
abstract: 
postStatus: publish
---
09 July 2013

A lot of people, including myself, felt (feel?) deeply betrayed by Microsoft’s rather abrupt dismissal of what some of us thought was the best client-side dev platform they’ve ever come up with: Silverlight.

Perhaps even more people are worried about the future of WPF in the face of Microsoft’s obvious focus on the new Windows Runtime (WinRT) at the expense of the Desktop (Win32) technologies such as Windows Forms and WPF.

I’m a little more sanguine about this than many people.

I never really bought into the idea of Silverlight as a cross-platform technology. I know, I know, Microsoft made it work on some flavors of OS X. But they didn’t take it to Linux or Android, and Apple blocked them from ever going to the iPad or iPhone. And honestly, *you have to follow the money*. Companies don’t exist to do good, they exist to make money, and Microsoft didn’t charge for Silverlight and so only stood to *lose* money by enabling us to build apps that ran on non-Windows devices just as well as Windows devices.

(as an aside, this is why I never get too upset when Google drops yet another free service – the way I look at it is that I’m exploiting the hell out of Google’s free stuff as long as they have it, and when they decide to drop a free service I just have to start paying for something I *should*have been paying for the entire time (but didn’t have to thanks to Google’s amazing “business” model)).

I *did* buy into the idea of Silverlight as a much safer and easier-to-deploy way of building Windows smart client apps. So to me the truly sad part about Silverlight going away is that it pushed us back toward creating apps that aren’t as safe (out of the sandbox), and that are slightly harder to deploy (ClickOnce).

Perhaps I’m unusual, but I really do buy into the idea that smart client apps don’t need the ability to reformat people’s hard drives, or alter system files, or snoop through my personal documents without my knowledge. In other words, the full client-side .NET/WPF/Windows Forms/Win32 technology stack just isn’t necessary for 99% of the apps I want to build and/or run, and after a few decades of dealing with viruses and malware and other bad stuff, I’m about ready to be done with it!

So here we site, with Silverlight in maintenance mode so Microsoft will keep it running on their platforms for another decade, but without any real assurance that it will continue to work on the Mac. And frankly I don’t really care, because I always thought the Mac was a lark.

To me where we are is simple:

- Microsoft is treating all of Win32/.NET on the client as legacy, so Windows Forms, WPF, and Silverlight are in the exact same boat
    - They are all stable (essentially unchanging) into the foreseeable future
    - They are all good/viable Win32/Desktop client technologies
    - They will ultimately fade away
- Microsoft is putting all their energy/money into rapidly bringing WinRT up to speed
    - Being a fan of “follow the money”, I expect that we’ll all eventually move to WinRT
    - WinRT 8.1 shows some good XAML/C# improvements over 8.0, demonstrating Microsoft’s commitment to making this a viable platform
    - WinRT still has a fundamentally flawed deployment/licensing model for business apps, and until they fix this WinRT is pretty much useless for business
    - WinRT still lags in XAML features behind Silverlight 5, but it is catching up
    - WinRT (like Silverlight) will hopefully *never* do everything WPF does, because then we’d be back to the same malware hell-hole we’re in with Win32


In short, for everyone wishing and hoping for Microsoft to put more energy/money into WPF (or even more far-fetched into Silverlight) I think the answer is that THEY ARE – but they are doing it via WinRT, by eventually providing a viable XAML/C# platform for business development on Windows that escapes the baggage of legacy Win32/.NET/Desktop.

We just need to do two things

1. Be patient, because WinRT is a v1 technology and will take a little time to mature
    1. Something I’m not worried about, because most businesses are just now getting to Win7 and won’t go to Win8 for a couple more years, so there’s some time for Microsoft to get their act together
2. Keep the pressure on Microsoft to bring WinRT to the level we need
    1. In terms of licensing/deployment models
    2. In terms of technology capabilities


Let’s face it. Either Microsoft (with us pushing/prodding/helping) provides a viable WinRT platform for us in the future, or we’d better all start learning JavaScript and/or Objective C…
