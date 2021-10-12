---
title: Windows 8, BYOD, and AD membership
postDate: 2012-04-23T11:10:41.2156763-05:00
abstract: 
postStatus: publish
---
23 April 2012

Microsoft recently posted some details regarding the way Windows 8 (specifically ARM-based tablets running Windows RT) will work in a domain.

http://blogs.msdn.com/b/b8/archive/2012/04/19/managing-quot-byo-quot-pcs-in-the-enterprise-including-woa.aspx

This related article from Steven Vaughan-Nichols suggests that Microsoft’s strategy is flawed:

http://www.zdnet.com/blog/networking/windows-8-tablets-not-open-for-business/2261?tag=nl.e539

And he could be right, but I think there’s substantial room for hope.

I *speculate* that Microsoft is thinking along the following lines:

1. If a company buys a Win8 tablet for an employee, they’ll probably buy an Intel-based tablet so it can be a tablet and also a laptop (with a keyboard/mouse), and most importantly so it can run existing line of business applications required for the employee to do their actual work.

I have such a tablet today, and I truly love the fact that it is a tablet *and a laptop* so I get the best of both worlds. It is wonderful!

And it can join an AD domain, and probably *should* join the domain, because it is corporate property.
2. If a person buys a Win8 tablet for themselves, they may well buy a cheaper and lower-powered ARM-based tablet. Such a device is a tablet, I suspect most will also double as a laptop with Office 15 (with a keyboard/mouse) – but they won’t be able to run existing line of business applications because those applications are Windows Forms or WPF or Silverlight.

A person, spending their own money to buy a device, is probably going to be unwilling to allow their corporate IT folks to set policies and perform administration tasks *on their personal device*. If my company wants to muck around with my devices, they can buy me the device! The last thing most people would ever want is for corporate IT to muck around with their own personal property.

So the fact that a Windows RT tablet can’t join a domain might be a true blessing. Microsoft is doing us a favor by eliminating the *possibility* that your corporate IT might insist on managing your personal property – because it just doesn’t work that way.


I’ve talked to people quite a lot over the past few months, about a possible dystopic future where employees are *required* to buy and support their own devices. All you have to do is take BYOD to its logical conclusion, and things look (to me) quite bleak. Surprisingly I’m finding that quite a few people in our industry thing this could be a *good thing*.

So here’s my train of thought.

One reason companies like BYOD is that the cost of computing shifts from the company to the employee. The company no longer has to buy the employee a laptop, because the employee *chose* to shell out $800 to get an iPad, and then *insists* that they be able to use it at work. As a result, IT can just say “OK, use it, but we don’t really support it”, and away you go. The company saves hardware and software purchase, licensing, and support costs. The burden of having a machine on which to do work falls on the employee – including the costs of acquisition, licensing, software, and support.

Now we’re not *quite* to that point yet. But I have heard CIO or IT director level people say, in so many words, that they see this BYOD thing as a way of cutting costs. So they are thinking exactly along this line, and it is a small step from employees *insisting* that they get to use their own devices, to employers *requiring* that employees supply and use their own devices.

And this is important, because true BYOD is incredibly expensive! In the long run, it means that all line of business apps must either be written in the highly volatile HTML 5 world, and tested on every conceivable device. Or they must be written and tested numerous times – in .NET, Objective C, Java, etc.

Magenic does quite a lot of mobile development these days, targeting iOS and Android mostly. And every time we get an Android project we have to go buy a whole new set of tablets for testing – because that platform is changing so fast, and is so inconsistent across devices and OS versions. This is true for native and HTML 5 apps – in all cases we have to test across a wide array of devices due to differences in the hardware, OS, and/or browsers.

So I feel confident saying BYOD is extremely expensive. And that might be fine if IT can figure out how to offset that expense. One way to help do that is to entirely eliminate the costs associated with hardware, OS, and support by shifting that responsibility to employees.

“You want to work in our shipping department for $17/hr? Great! Just make sure to bring your $800 iPad to work on Monday when you start. Oh, you don’t have an iPad? You don’t have $800 laying around? Well sorry, then you can’t work here.”

You think this won’t happen? Maybe not. I *hope not*.

But at some point IT is going to have to justify and/or offset the costs of BYOD. At some point in the next couple years the CEO/CFO or board of directors is going to ask why IT costs have spiraled out of control, and the answer will be “because you said we had to support the iPads used by our executives”. At that point the proverbial sh\*t will hit the fan, and some IT directors will lose their jobs, and BYOD will come to a sudden and inglorious end.

In the meantime, we can all be happy that there’s no way IT can join our Windows RT tablets (or iPads or Kindle Fires) to the AD domain. Because those are *our personal property* and shouldn’t be subject to corporate administrative policies and more than our cars, our televisions, or our other personal property.
