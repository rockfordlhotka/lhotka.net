---
title: Windows 8 LOB deployment &lsquo;story&rsquo;
postDate: 2013-01-29T22:57:03.478-06:00
abstract: 
postStatus: publish
---
29 January 2013

*Note that this is one post in a series. Make sure to read them all. [This post](http://www.lhotka.net/weblog/Windows8WinRTSideloadingUpdate.aspx) provides an index to the set.*

This is the second blog post covering the basics around deployment of business apps (LOB apps) on Microsoft’s new Windows Runtime (WinRT) platform. The [first post focused on direct costs](http://www.lhotka.net/weblog/CostToEnableSideloadingOnAWindows8Device.aspx), this one focuses on different business scenarios.

In my view the deployment story for business apps targeting WinRT is not currently good. I’ll break the story into parts depending on your scenario:

- Developer/tester
- Large enterprise
- Medium enterprise
- Small business
- Home users (employees who work from home sometimes)


Before I get into these scenarios I want to cover the use of the Microsoft Store for business app deployment.

### LOB deployment via Windows Store

A Microsoft employee suggested that what I should be recommending is that people deploy their business apps through the Windows Store. So let’s think about this a little bit, because I don’t think it is real workable.

First, suppose I build a mission-critical business app in WinRT and submit it to the store. Around 8 days later (give or take a week) the app will be approved and available from the store. My users start using the app and then we discover a bug, or a critical regulatory feature change, or some other scenario where the app is useless until fixed. So we fix the app and 8 days later (give or take a week) the update is available for my users. So during that 8+ day period what happens? Do we revert to a manual process? Do we just lose money? Do we send employees home? Obviously the store is *useless* for any important business app deployment scenarios.

Second, I build my non-mission-critical (really unimportant) business app in WinRT and submit it to the store. The store approval process requires that Microsoft employees manually run each part of the app. So do I give them access to my live data? My staging servers? Do I set up servers just for the Microsoft certification process? How much extra code/functionality in the client app and/or server-side infrastructure is necessary to enable Microsoft’s people to test my app? And what legal recourse do I have if Microsoft accidentally leaks my proprietary data or my trade secrets? Do I get to sue Microsoft if their disgruntled tester makes off with some of my key IP and ruins my business or my reputation? Again, the store is totally unacceptable for business app deployment scenarios.

Given that backdrop, the only alternative is ‘side-loading’. This means deployment of apps directly to computers, workstations, PCs, devices – without going through the store.

My previous blog post covers the various side-loading options, but not from a business scenario perspective such as developer/tester, large enterprise, small business, etc.

Let’s look at each scenario in turn.

### Developer/tester

If you are a developer or tester the deployment story is actually quite good. In Visual Studio 2012 you can run a wizard that will create an appx package and associated ps1 (powershell) script that can be used to install your WinRT app on any Windows 8 machine (Windows RT, Windows 8, Windows 8 Pro, Windows 8 Enterprise). The app will work for a few weeks before the developer key and/or app test certificate expires – which is fine for dev/test purposes.

You can also use the remote debugging tools in Visual Studio to deploy an app to your Windows 8 machines, and you can then attach your debugger remotely. For example, you can debug your app while it is running on a Windows RT tablet – all from your primary dev workstation. Very nice!

### Large enterprise

If you are part of an enterprise that meets the following constraints there’s the start of a pretty decent WinRT LOB deployment story:

1. All your workstations run Windows 8 Enterprise
2. All your workstations are joined to your domain
3. You already use Microsoft System Center to manage and deploy programs to your workstations


In this case you can push a group policy to your domain-joined Win8 Enterprise workstations to enable side-loading of WinRT apps, and you can push those apps to the workstations using System Center. Obviously this requires a pretty mature IT staff, procedures, and infrastructure, but that is true of most large enterprises.

So far so good. But most large enterprises will also have Windows RT tablets, and the story is a little different for these devices because they can’t join your domain, and aren’t running Win8 Enterprise.

For non-domain devices (Windows RT, Windows 8 Pro, Windows 8 Enterprise) you need to buy a special side-loading key for each device at $30 per device. These licenses are sold in packs of 100, which is probably not a big deal for an enterprise. You must install these keys on each device – no reuse or transfer of a key is allowed. Then you can purchase an InTune add-on for SCCM and pay $4/device/month that allows you to manage and deploy apps to the non-domain devices.

My [device cost calculator spreadsheet](https://skydrive.live.com/?cid=b9397700a0a08439&id=B9397700A0A08439%21318#!/view.aspx?cid=B9397700A0A08439&resid=B9397700A0A08439%215643&app=Excel) can help you figure out the cost for your organization to cover the $30 unlock keys and InTune subscription costs.


> **Update: **More info from Microsoft indicates that if you have an EA and Software Assurance (SA) then your domain joined Windows 8 Enterprise machines come with a "companion license" allowing you to unlock one Windows RT device without the added $30 fee. Presumably you'd talk to your EA account rep to get these companion keys.


If you add all these costs, you can see that it will cost 10’s of thousands of dollars (or more) to install and update WinRT apps across your enterprise. Realistically probably 100’s of thousands of dollars. So you might ask why you’d pay all that money when you could keep using WPF and ClickOnce for no additional charge. My only answer is that in a large enterprise perhaps a few hundred thousand dollars isn’t a big deal? (yes, that was sarcasm)

### Medium enterprise

If you are part of a medium enterprise the story is generally worse. In these types of business the following is probably true:

1. You have a mix of Windows 8 Pro and Windows 8 Enterprise
2. Not all workstations are joined to the domain
3. You probably don’t have a full Microsoft System Center infrastructure in place


Remember that only domain-joined Windows 8 Enterprise machines can use group policy to enable side-loading. All non-domain machines require a $30 per device side-loading key to unlock this feature (again, sold in packs of 100). This is also true of Windows RT devices of course. Surprisingly, it is also true of domain-joined Windows 8 Pro machines – they still need the $30 unlock key.

So imagine you have 240 domain-joined Win8 Enterprise machines – you can unlock them for side-loading and use SCCM plus InTune for deployment. If you don’t have SCCM fully in place then you might need to use sneaker-net to deploy and update your WinRT apps by running PowerShell scripts on each device.

Then imagine you have 40 domain-joined Win8 Pro machines. For these you need to buy 100 unlock keys ($3000) and manually unlock side-loading on each machine. Again, you’ll need SCCM+InTune or sneaker-net PowerShell deployment to get the apps installed and updated over time.

Finally, imagine you have 170 Windows RT devices – most probably not owned by your company, but by employees. You’ll have to buy 200 unlock keys ($6000) and manually unlock side-loading on each device. Remember that these keys aren’t transferable, so when an employee leaves, or chooses to replace their device, you’ll lose (and often need to replace) that unlock key. Obviously this will require some sort of key management scheme ([Magenic](http://www.magenic.com) is happy to help you write a custom solution of course ![Smile](binary/Windows-Live-Writer/5c6ef98d052c_D21C/wlEmoticon-smile_2.png) ).

For *all* these machines/devices you will need SCCM+InTune, or have an IT intern or someone run around and unlock PowerShell so people can run scripts. Then perhaps you can train at least some of your users to run the PowerShell scripts from a network share to install/update the apps.

The InTune add-on for SCCM costs $4/device/month, on top of the $30/device unlock key cost. My [device cost calculator spreadsheet](https://skydrive.live.com/?cid=b9397700a0a08439&id=B9397700A0A08439%21318#!/view.aspx?cid=B9397700A0A08439&resid=B9397700A0A08439%215643&app=Excel) can help you figure out the cost for your organization to cover the $30 unlock keys and InTune subscription costs.

Odds are you’ll look at this and ask why you have to spend many thousands of extra dollars to replace WPF and ClickOnce (no unlock fees, no manual processes, etc). And I can’t argue with you – I can’t see how any medium sized business would write a WinRT LOB app at this point.

### Small business

If you are part of (or more likely the owner of) a small business the story is pretty much non-existent. In this case the following is probably true:

1. You have a mix of Windows 8 and Windows 8 Pro
2. You have no domain
3. You have no Microsoft System Center
4. You have no IT staff beyond the “consultant” you bring in a couple times a year to fix network or printer problems


First off, the Windows 8 edition of Windows 8 *can not do side-loading* so it is impossible to deploy business apps on those machines. Microsoft tells me that you should have bought Win8 Pro in the first place, and that it is technically illegal to use Windows 8 for non-personal use. So you’ll need to upgrade those machines to Windows 8 Pro.

Next, you’ll need to buy the $30 unlock keys in packs of 100 for your Win8 Pro machines. You probably have around 20 computers, so that’s $3000 – more like $150 per machine than $30, but at least you have enough keys to accommodate future growth? And of course you’ll need to manually install the side-loading keys, unlock PowerShell, and use sneaker-net to install/update your WinRT apps.

The same is true for the handful of Windows RT tablets you or your employees are using. That’s another $3000 to get 100 unlock keys. You probably only have 8 such devices, so that’s a mere $375 per device. Again, the whole manual unlock, install, update process must be handled.

As a result, I can’t see where any small business would ever consider building a WinRT business app. It is way cheaper to keep building apps in WPF or PHP or whatever you are using today.

### Employees working from home

The final scenario is cross-cutting, in that large, medium, and small businesses all have employees who occasionally (or frequently) work from home using their own personal computers.

Most of these personal home computers are retail purchases, and so run Windows 8. Not Pro or Enterprise. As a result they *can not side-load apps* and therefore can’t run WinRT business apps at all.

One interpretation of this move is that Microsoft has decided that we all work too much, and they are helping us achieve a better work-life balance by making it unrealistic to work from home.

Another interpretation is that they want employers to spring for the upgrade fees (plus the $30 per device) to get all home computers running Windows 8 Pro and unlocked for side-loading. It is a great way to potentially double the licensing revenue of Windows on a per-employee basis I suppose.

Or perhaps the thought is that nobody buys home computers anymore, and that we all bring our work laptops home with us to work at home. I suppose this is pretty valid, given that a lot of people have quit purchasing home PCs because they have Macs or iPads and Xboxes for gaming?

Yet another theory is that Microsoft wants all businesses to set up a HyperV server farm so home users can RDP into virtual Windows 8 Enterprise machines to do their work from home.

Personally none of these make much sense to me.

In any case, this is the first time in the history of Windows (going all the way back to around 1990) where am employee can honestly tell their boss that they can’t bring their work home with them because their home computer *isn’t legally allowed* to run the business software necessary to do work.

### Summary

Right now it appears that Microsoft has worked very hard to devise a licensing and deployment scheme for WinRT apps designed specifically to discourage the creation of any WinRT business apps. Whether this is intentional or accidental I can’t say, but it is surely the case that no responsible business or IT manager could look at these scenarios and think that a move to WinRT for business app development makes sense at this time.

Hopefully Microsoft examines their current scheme and recognizes the severe disincentive they’ve created for WinRT development, otherwise I see a very long and bright future for WPF, ASP.NET, and PHP.
