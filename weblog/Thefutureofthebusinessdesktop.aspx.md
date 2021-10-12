---
title: The future of the business desktop
postDate: 2013-12-01T21:16:15.0710404-06:00
abstract: 
postStatus: publish
---
01 December 2013

This recent article is interesting:

http://www.neowin.net/news/windows-xp-remains-nearly-flat-windows-881-up-slightly-in-novembers-os-data

Of course it is talking about the “now dead” traditional computing market. You know, the market that totally dominates the business desktop/laptop world, as well as (still) most home computing.

Although tablets and phones have enjoyed massive growth over the past few years, the reality is that they have done little to actually *replace* traditional computing in many ways.

Of course as soon as anyone makes statements or draws conclusions about anything to do with market share numbers between OSes and/or mobile devices the conversation instantly devolves into meaningless drivel. I think the reason these conversations are almost always fruitless is that there's a lack of definition around terms and the nature of the conversation.

I want to be clear that this entire blog post is about *smart client* development. If you are already building all your business software as web sites then you don’t really care much right? The client device is merely a colorful terminal for your server-side computing, and for the most part it doesn’t matter what OS or brand device is being used as long as it has a modern browser to act as that terminal.

But from a smart client perspective the client device and OS matters a lot!

The primary focus in my career, and at [Magenic](http://www.magenic.com) is business app dev, and tablets have done little to *replace*traditional computers in the workplace thus far. They augment, but they don't replace. Hence the workplace computing space is still roughly 91% Windows.

People have tablets at home, and for a lot of home scenarios they are replacing traditional computers. And tablets are used in some limited business scenarios, mostly where employee’s jobs are made more efficient if they have computing while away from their desks. This is what we currently refer to today as "mobile" for the most part. This segment might be transitioning to tablets in a way that eats into computer sales, but even that isn't entirely clear. Anyone who brings a lot of work home almost certainly still has a home computer in addition to their tablet, and I still see a lot of “mobile workers” carrying around laptops or ultrabooks.

And then there's the pure consumer market, which is essentially entirely mobile, or will be soon. People who don't bring work home with them have little or no need for a computer other than to run iTunes. If Apple had iTunes for the iPad itself I suspect a massive number of people wouldn't need a PC or Mac – as long as they don’t bring work home with them (or if their work doesn’t require data entry or manipulation).

For my part I’ve spent my career in the business space, not the consumer space. And I don’t see myself getting rich building inventory management apps that sell for $0.99 per user. Instead I create inventory management systems for companies that pay hundreds of thousands or millions of dollars for such software. Then those companies expect that software to run for 7-10 years so they can recover their investment. This is almost entirely unlike the consumer app space.

What makes this interesting is that there's a broad assumption in the world at large that the PC as we know it is done for - that it will be replaced by "something else". This is bolstered by Microsoft's own moves that effectively deprecate the "desktop" in favor of a different approach.

That said, I am 110% certain that 20 years from now there'll still be "desktop" (Win32, .NET, etc.) apps - and people will use them from a terminal emulator (probably RDP into Citrix) via their then-current device and OS. Exactly like so many old mainframe/minicomputer apps are used today via 3270 or VT terminal emulators via Windows.

But I personally don't want to be a maintenance developer on one of those soon-to-be-ancient apps, and so to me the 60 bajillion dollar question is what (if anything) will eat into the 91% business OS market share currently dominated by Windows. It might be one of these options:

1. Windows (presumably in the form of WinRT, assuming Microsoft fixes their flawed [business app side loading cost model](http://www.lhotka.net/weblog/Windows8WinRTLicensingIdeas.aspx))
2. "JavaScript"/TypeScript/etc. (assuming an offline deployment model for apps, including some js version of Excel that'd work offline)
3. Android (again, assuming Android continues to expand into bigger and multiple monitors, and Office eventually gets spun off into a business so Excel works on Android)
4. iOS (assuming iOS expands to handle multiple 30" monitors and Microsoft spins off Office so they fully support iOS with Excel)
5. Windows Desktop (perhaps everything we're going through right now is a fad - a fluke - and "real work" will be done on Windows long into the future)


Personally I assume that what we think of as "mobile" today will disappear as it merges into the business "desktop" of the future, leaving us with the same old [business vs consumer spaces](http://www.lhotka.net/weblog/ConsumerVsBusinessApps.aspx).

And as a business developer I won't care any more about the consumer space in the future than I have in the past. Which is to say not at all, beyond being a user of consumer apps myself (I do enjoy email, calendar, Instagram, Facebook, etc.).

But I *will*care about "mobile" because it will (imo) *become* the future business platform. *Something* will end up eating into and ultimately replacing today’s 91% Windows business desktop market.

I still think WinRT has a shot at this. A good shot actually given that the networking and security infrastructure to support Windows is already dominant, so the *easiest* thing for most businesses would be to slowly shift to WinRT. Again, presupposing Microsoft wakes up and fixes their ridiculous business app side loading model.

I also think JavaScript ([TypeScript](http://www.typescriptlang.org/), Angular, Knockout, etc.) has a good shot, especially if Chrome continues to mature its offline deployment story and Microsoft continues to create an artificial barrier to WinRT adoption by charging a "deployment tax" for WinRT business apps. I could totally see most business apps being built to assume Chrome on the client, because Chrome runs on every type of device/OS people are likely to have.

I am dubious that Android has a shot, but I don't discount it. Today you can buy 24" Android "desktops", so some Android vendors are certainly trying to adapt the devices, OS, and its ecosystem to the business world.

I am even more dubious about iOS, because I have yet to see Apple making any moves necessary to become a business/enterprise player at a device or OS level.

And I didn't mention OS X or Linux here because they've had nearly 20 years to become players and have yet to get more than 5% of the total market, so why would we think the future would be different? Though I must admit that [Ubuntu](http://www.ubuntu.com) and [Mint](http://www.linuxmint.com) are very usable user-focused Linux implementations, and if they’d have existed 15-20 years ago Windows would have been in trouble.

As a result I’m personally continuing to invest in C# and XAML in the hopes that Microsoft makes WinRT a viable smart client platform. And I’m investing in TypeScript, JavaScript, and various related frameworks because I think that platform is probably the next most likely to become the smart client business platform of the future.
