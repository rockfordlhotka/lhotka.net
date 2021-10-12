---
title: Microsoft identities - argh!
postDate: 2017-02-08T12:51:54-06:00
abstract: 
postStatus: publish
---
08 February 2017

The concept of identity with Microsoft services is a mess, something I probably don't have to tell any Microsoft developer.

Some services can only be attached to a personal Microsoft Account (MSA), and other services can only be used from an AD account. For example, MSDN can only be directly associated with an MSA, while Office 365 can only be associated with an AD account. Some things, like VSTS, can be associated with either one depending on the scenario.

I used to have the following:

- r\_\_\_y@lhotka.net - MSA with my MSDN associated
- r\_\_\_y@magenic.com - Magenic AD account
- r\_\_\_y@magenic.com - MSA with nothing attached (I created this long ago and forgot about it)


That was a total pain when I started using O365 and an AD-linked VSTS site with my r\_\_\_y@magenic.com AD account, because Microsoft couldn't automatically distinguish between my AD and MSA accounts; both named r\_\_\_y@magenic.com. As a result, every time I tried to log into one of these sites they'd ask if this was a personal or work/school account.

Fortunately you can [rename an MSA](https://support.microsoft.com/en-us/help/11545/microsoft-account-rename-your-personal-account) to a different email address. I renamed my (essentially unused) r\_\_\_y@magenic.com account to a dummy email address so now I really just have two identities:

- r\_\_\_y@lhotka.net - MSA with my MSDN associated
- r\_\_\_y@magenic.com - Magenic AD account


This way Microsoft automatically knows that when I use my AD login that it is a work/school account and I don't have to mess with that confusion.

There's still the issue of having MSDN attached to an MSA, and *also* needing to have some connection from my AD account to my MSDN subscription. This is required because we have VSTS sites associated with Magenic's AD, so I need to log in with my AD account, but still need to ensure VSTS knows I'm a valid MSDN user.

Here's info on how to [link your work account to your MSDN/MSA account](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/link-msdn-subscription-to-organizational-account-vs).

At the end of the day, if I'd never created that r\_\_\_y@magenic.com MSA account (many years ago) my life would have been much simpler to start. Fortunately the solution to *that* problem is to rename the MSA email to something else and remove the confusion between AD and MSA.

The MSDN linking makes sense, given that you need an MSA for MSDN, and many of us need corporate AD credentials for all our work sites.
