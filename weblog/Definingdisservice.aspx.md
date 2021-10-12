---
title: Defining disservice
postDate: 2014-03-02T22:55:12.5533454-06:00
abstract: 
postStatus: publish
---
02 March 2014

In my last post my focus was on listing [the numerous WinRT apps I use](http://www.lhotka.net/weblog/TopWin8WinRTApps.aspx) on a regular basis – many of which, if I couldn’t get them on Win8 would drive me to carry an iPad. I’m personally not just a software developer, I’m a *user* of computing as well.

One line, a sensation-maker, in my post was that I think Windows developers who aren’t using WinRT apps are doing their ultimate users a disservice. This doesn’t apply to web developers or other people who aren’t developing actual Windows applications, but it surely applies to people living today in the legacy WPF, SL, and Windows Forms technologies.

The thing is, I made no effort to describe *why* I believe that to be true, because the focus of that post was to list useful apps.

So what *did*I mean by that comment?

Here’s the thing. As someone who *does* use a lot of WinRT apps I can say that a lot of them suck. I’ve divided the suckage into three categories.

Some apps are obviously **built by pure mobile developers**, who have no comprehension of keyboard/mouse or productivity on anything but a tablet. So their apps are sometimes pretty good on a tablet, but are virtually useless on a laptop or desktop. Because I use all three types of device with pretty much every app, I find that these mobile-only or mobile-first apps just suck. I *might* use them on my tablet, but they are always pretty secondary to more complete apps because they aren’t universal.

Other apps are obviously built by **pure desktop developers**, who have no comprehension of touch. These apps often work pretty well with keyboard/mouse, but are awkward to use with touch. Technically they *work* on my tablet, but they aren’t fun or efficient, and so I consider them to suck.

The third group of sucky apps are built by **people with no WinRT user experience**. These apps might, in theory, work pretty well with touch and/or keyboard and mouse, but they miss the point of all the cool WinRT features. They don’t use AppBars or the Share charm or Settings or Search correctly. They don’t use dialogs correctly, they don’t use navigation correctly. I’m sure the authors of these apps often think they are being clever by inventing their own techniques, but as a *user* their apps just suck because they don’t work right.

In short, sucky apps come from three sources:

1. Mobile developers who don’t consider laptop/desktop device scenarios
2. Desktop developers who don’t consider tablet scenarios
3. Developers who are ignorant about the WinRT environment and don’t understand how it works


So as a developer, if you plan to ever build WinRT apps and you aren’t using WinRT then you are pretty much guaranteed to fall into category 3, and very possibly 1 and/or 2.

Hence, if you are a smart client developer – unless you are planning to retire on WPF (which is fine) or switch to the iPad/Android world, you are doing yourself and your users a disservice if you aren’t actually using and learning “the WinRT way”.

**Update:**

Jason Bock mentioned something to me that got me thinking. I base all of this on one core assumption:


> *Win32 has no long-term future as a mainstream technology.*


To be clear, I am 100% sure Win32 will be around for the next 20-30 years, just like mainframes and minicomputers are still with us – usually hidden behind the scenes or in a terminal window, but still here. I don’t think anyone would call them “mainstream” though. Nobody ever mentions IBM in the same breath as Microsoft/Apple/Google/Samsung.

Now if you think Microsoft will back off from WinRT, and by some miracle Apple and Google and Samsung will just completely fail to adapt iOS, Android, or ChromeOS to the enterprise, then you can imagine yourself still doing Win32 as a mainstream technology in 5-7 years.

I personally can’t imagine that happening. I think 5 years from now Win32 will be pretty much what we think of as VB6 today. Something that runs a ton of software, and something that people still do, but not something that would be considered mainstream or vibrant.

For my part, I think that if Microsoft *does* back off WinRT to try and rejuvenate Win32 … well … that’ll be the opening one or more competitors needs to swoop in and take the enterprise desktop.
