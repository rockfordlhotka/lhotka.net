---
title: Silverlight is &ldquo;dead&rdquo;
postDate: 2012-12-07T11:23:33.5868451-06:00
abstract: 
postStatus: publish
---
07 December 2012

The Silverlight.net web site is apparently now gone, merged into the broader msdn.com ecosystem (where it belonged in the first place imo):

http://www.zdnet.com/microsoft-pulls-the-plug-on-its-silverlight-net-site-7000008494/

As we’ve known now for a long time, Silverlight is “dead”. It is in support mode and will be for a decade.

Just like Windows Forms has been since 2005, and WPF is now as well (do you really think Microsoft is going to divert money from WinRT to do *anything* with WPF at this point??? If so I’ve got this beachfront property for sale…).


> *As an aside, ASP.NET Web Forms also “died” in 2005, but recently got a major infusion of money in .NET 4.5 – showing that even a “dead” technology can receive a big cash investment sometimes – though it still isn’t clear that this will be enough to breath any new life into Web Forms for most organizations. I suspect it is more likely that this recent investment will just allow organizations with massive Web Forms sites to keep them limping along for another 5-10 years.*


If a technology is defined as “dead” when its vendor stops enhancing it and starts maintaining it while they put most of their money into the future, then I must say that I’ve spent pretty much my entire ~25 year career working on dead technologies. And it has been fun! ![Smile](binary/Windows-Live-Writer/Silverlight-is-dead_9AEB/wlEmoticon-smile_2.png)

Although some of us tech geeks like to jump to the next *potential* upcoming thing, the people who actually fund software projects rarely want to accept that kind of risk. They generally *prefer* to build applications on stable technology. Most stable technology is “dead” or “dying” based on this idea of “live” technology being rapidly changing and evolving.

Obviously there’s a fine line here.

Target stable technology that is too old and you really are in trouble. Windows Forms is an example of this, because its underlying technology has no migration path to a WinRT future. Although a *lot* of organizations have massive investments in Windows Forms, I would hope that they’d shy away from starting new development on this extremely stable, but now too old, technology.

Target stable technology that is new, but old enough to be stable and life is generally pretty good. WPF and Silverlight (for smart clients, not for cross-platform RIA) are examples of this. The reason is that these technologies (especially Silverlight) have a good migration story to a WinRT future. A lot of organizations are investing in WPF, and that’s good. But I’d be shocked if Microsoft invests anything in WPF going forward – its future is the one Windows Forms has enjoyed since 2005 – stable maintenance of the technology. *Perfect* for building critical business apps. Organizations also have large investments in Silverlight, and as long as the intent was smart client development (not cross-platform RIA) it seems to me that they are in the exact same place as everyone using WPF. Arguably better, because Silverlight is much closer to WinRT than WPF.

http://magenic.com/Portfolio/WhitePaperWindows8DevelopmentPlatform.aspx

If you are using Silverlight for cross-platform rich web development, then I do agree that the news is not good. The current alternative appears to be HTML 5, though it is also clear that this is an expensive alternative with an unsure future. Just like every other silver bullet to write once and run anywhere, I think you have to go into such a venture expecting a lot of cost and pain. There’s no widely successful example in the history of computing that indicates otherwise…

The final option is to target “live” technologies. You know, the ones where vendors *are* dumping huge amounts of money, and where the technology and platform are changing rapidly. Things like HTML 5 and WinRT are examples of this. As a tech geek I *love* it when organizations want to do this sort of thing, because the challenge is high and we all get to learn a lot of new stuff. Of course the development costs are also quite high because we’re getting paid to learn this new stuff. And the overall costs for the software are high because the technology/platform isn’t stable and the app probably needs to be rewritten (in whole or part) every few months to deal with platform changes.

Some organizations are willing to accept the costs and inconvenience associated with using “live” technologies. But most organizations don’t have the time or money or risk tolerance, and are far better off targeting “dead” technologies like WPF and Silverlight. They just need to be careful to have strategic migration plans so they can get off those technologies before they reach the point of where Windows Forms is today.
