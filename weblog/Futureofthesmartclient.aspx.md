---
title: Future of the smart client
postDate: 2013-04-04T09:44:57.463-05:00
abstract: 
postStatus: publish
---
04 April 2013

In 1991 I was a DEC VAX programmer. A very happy one, because OpenVMS was a wonderful operating system and I knew it inside and out. The only problem was that the “clients” were dumb VT terminals, and it was terribly easy to become resource constrained by having all the CPU, memory, and IO processing in a central location.

This was the time when Windows NT came along (this new OS created by the same person who created OpenVMS btw) and demonstrated that PCs were more than toys – that they could be considered real computers. (yes, this is my editorial view ![Smile](binary/Windows-Live-Writer/Future-of-the-smart-client_8098/wlEmoticon-smile_2.png) )

From that time forward my personal interest in software has been expressed entirely via distributed computing. Sure, I’ve built some server-only and some client-only software over the past 22 years, but that was just to pay the bills. What is *interesting* is building software systems where various parts of the system run on different computers, working together toward a common goal. That’s fun!!

This type of software system implies a smart client. I suppose a smart client isn’t strictly *necessary*, but it is surely ideal. Because most software interacts with humans at some point, a smart client is ideal because that’s how you provide the human with the best possible experience. Obviously you can use a VT terminal or a basic HTML browser experience to provide this human interface, but that’s not *nearly* as rich or powerful as a smart client experience.

For the past couple decades the default and dominant smart client experience has been expressed through Windows. With smart client software written primarily in VB, PowerBuilder, and .NET (C#/VB).

The thing is, I am entirely convinced that our industry is at a major inflection point. At least as big as the one in the mid-1990’s when we shifted from mainframe/minicomputer to PC, and when n-tier became viable, and when the infant web became mainstream.

Prior to the mid-1990’s computing was chaos. There were many types of mainframe and minicomputer, and none were compatible with each other. Even the various flavors of Unix weren’t really compatible with each other… Software developers tended to specialize in a platform, and it took non-trivial effort to retool to another platform – at least if you wanted to be really good.

Over the past couple decades we’ve been spoiled by having essentially one platform: Windows. Regardless of whether you use VB, PowerBuilder, .NET, or Java, almost everyone knows Windows and how to build software for this one nearly-universal platform.

Now we’ve chosen to return to chaos. Windows is still sort of dominant, but it shares a lot of mindshare with iOS, OS X, Android, and ChromeOS. We appear to be heading rapidly into an environment more like the late 1980’s. An environment composed of numerous incompatible platforms, all of which are viable, none of which are truly dominant.

There is one difference this time though: JavaScript.

Please don’t get me wrong, I’m not a rah-rah supporter of js. I am *extremely* skeptical of cross-platform technologies, having seen countless such technologies crash and burn over the past 25+ years.

But there’s an *economic* factor that comes to bear as well as technical factors. Unlike in the late 1980’s when computing was important but not critical to the world at large, today computing *is critical to the world at large*. Individuals and organizations can not function at the levels of productivity we’re used to without computing and automation.

In other words, in the late 1980’s we could afford to be highly inefficient. We could afford to have a fragmented developer space, split by myriad incompatible platforms.

Today the cost of such inefficiency is much higher. I suspect it is too high to be acceptable. Think about your organization. Can you afford to build every client app 3-6 times? Will your board of directors or company owner accept that kind of increase in the IT budget?

Or can you afford to pick just one platform (iOS, Windows, whatever) and tell all your employees and partners that you only work with that one type of device/OS?

(btw, that’s what we’ve done for the past 20 years – we just tell everyone it is Windows or nothing, and that’s been working well – so such a move isn’t out of the question)

Let’s assume your organization can’t afford a massive increase in its IT budget to hire the dev/support staff to build and maintain every app 3-6 times. And let’s assume we collectively decide to embrace every random device/OS that comes along (BYOD). What then?

I suggest there are two options:

1. Return to a terminal-based model where the client device is a dumb as possible, probably using basic HTML – to which I say BORING! (and awful!)
2. Find a common technology for building smart client apps that works reasonably well on most device/OS combinations


Personally I am entirely uninterested in option 1. As I said, I spent the early part of my career in the minicomputer-terminal world, so I’ve been there and done that. Boring.

The only technology that looks even remotely capable of supporting option 2 is JavaScript.

Is that a silver bullet? Is it painless? Clearly not. Even if you ignore all the bad bits of js and stick with [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742/) it is still pretty messy.

However, VB 1, 2, and 3 were also pretty immature and messy. But a lot of us stuck with those products, pushing for (and getting) improvements that ultimately made VB6 the most popular development tool of its time – for apps small and big (enterprise).

So sure, js is (by modern standards) immature and messy. But if the broader business development community sees it as the only viable technology going forward that’ll bring a lot of attention and money into the js world. That attention and money will drive maturity, probably quite rapidly.

OK, so probably not maturity of js itself, because it is controlled by a standards body and so it changes at a glacial pace.

But maturity of tooling (look at the amazing stuff Microsoft is doing in VS for js tooling, as well as TypeScript), and libraries, and standards. That’ll be the avenue by which js becomes viable for smart client development.

If it isn’t clear btw, I am increasingly convinced that (like it or not) this is where we’re headed. We have a few more years of Windows as the dominant enterprise client OS, but given what Microsoft is doing with Windows 8 it is really hard to see how Windows will remain dominant in that space. Not that any one single device/OS will displace Windows – but rather that *chaos* will displace Windows.

As a result, barring someone inventing a better cross-platform technology (and I’d love to see that happen!!), js is about to get hit by a lot of professional business developers who’ll demand more maturity, stability, and productivity than exists today.

This is going to be a fun ride!
