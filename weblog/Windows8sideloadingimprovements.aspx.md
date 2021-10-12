---
title: Windows 8 side loading improvements
postDate: 2014-04-03T01:43:38.6751348-05:00
abstract: 
postStatus: publish
---
03 April 2014

Microsoft has substantially improved the story around side loading of Windows 8 WinRT (Windows Runtime or Windows Store) apps for the enterprise and business environments.

I’ve [blogged pretty extensively](http://www.lhotka.net/weblog/Windows8WinRTLicensingIdeas.aspx) in the past about the costs of the two steps necessary to side load apps:

1. Unlock your devices for side loading
2. Actually side load (install) your various business apps


Microsoft has now radically changed the cost of step 1. [This blog post](http://blogs.windows.com/windows/b/business/archive/2014/04/02/building-the-mobile-workplace-with-windows-and-windows-phone.aspx) from Microsoft contains the following statement:


> ***Enterprise Sideloading**– In May, we will grant Enterprise Sideloading rights to organizations in certain Volume License programs, regardless of what product they purchase, at no additional cost. Other customers who want to deploy custom line-of-business Windows 8.1 apps can purchase Enterprise Sideloading rights for an unlimited number of devices through Volume Licensing at approximately $100. For additional information on sideloading licensing, review the*[*Windows Volume Licensing Guide*](http://download.microsoft.com/download/9/4/3/9439A928-A0D1-44C2-A099-26A59AE0543B/Windows_8-1_Licensing_Guide.pdf)*.*


Basically what this means is the following (as I understand it):

For developers/testers things are unchanged – you still use a free dev unlock key to install apps for development and testing.

For organizations with an Enterprise Agreement (EA) you’ll be able to get a side loading unlock key that you can use on all your Windows 8 Pro and Windows 8 Enterprise devices, regardless of whether they are domain joined or not. As before, you can also get ‘companion device’ keys to unlock Windows RT devices if you have a Windows 8 Enterprise device too.

For smaller organizations that don’t have an EA you might have (or can get) one of a number of ‘Open’ or ‘Select’ license agreements with Microsoft. Once you have one of these you can buy a side loading key for around $100 that will unlock any number of Windows 8 Pro or Windows 8 Enterprise devices.

When compared to the old model of buying keys for $30/device this is a major change in the right direction. For a maximum of around $100 virtually every organization (small to huge) can get a side loading unlock key for all their devices.

Now this still doesn’t address the need to actually install your apps onto your devices.

Microsoft offers InTune, which is a full MDM (mobile device management) product. If you find the value proposition of an MDM compelling then InTune is probably the right answer for you – though there’s a per device/per month cost (ranging from $6/device/month to $11/device/month) so you don’t get MDM for free of course.

[![Screenshot (5)](binary/WindowsLiveWriter/Windows8sideloadingimprovements_14DA4/Screenshot%20(5)_thumb.png "Screenshot (5)")](binary/WindowsLiveWriter/Windows8sideloadingimprovements_14DA4/Screenshot%20%285%29_2.png)I’ve been coordinating an open source project called [OrgPortal](http://github.com/magenic/orgportal) that you can use to (relatively) easily create an app store for your organization.

There’s another open source project called [CompanyStore](http://companystore.codeplex.com) that is very similar.

Alternately you can have your users manually run a PowerShell to install and update each app manually over time.

I think Microsoft has taken a substantial step in the right direction with the changes to the cost and availability of side loading keys. Couple this with the increasing maturity of projects like OrgPortal and CompanyStore and I think we’re getting to the point where WinRT is something to consider for business app development.
