---
title: Windows 8 CP install experience
postDate: 2012-03-05T20:20:26.5693505-06:00
abstract: 
postStatus: publish
---
05 March 2012

I’ve now installed the Windows 8 Consumer Preview four times on three machines.

**First**, I did a reimage of the tablet I got at //build/ last fall. That was a smooth and seamless process, and I’m really enjoying using Windows 8 on the tablet.

**Second**, I did an install into a VirtualBox virtual machine on my main desktop. This is not satisfying. The CP release is slower in VirtualBox than the Dev Preview was, and so I’ve already deleted the virtual machine. Clearly we’re at a point where a VM just isn’t going to cut it unless you are desperate. (the alternative is boot from vhd, and people seem to be having good luck with that)

In short, I don’t think I’ll mess with trying to run Win8 in a VM anymore.

**Third**, I did an upgrade of my Win7 laptop to Win8. This seemed to go very smoothly, but ultimately was a failure. Issues I encountered include:

- I couldn’t link my Magenic domain user to a Microsoft user, so some apps (like SkyDrive) just didn’t work at all, and others kept prompting me for credentials
- I couldn’t get a dev license from VS11 to debug Metro style apps in WinRT
- The login process took forever and a day – every time; I’m not sure what it was doing, but it was really slow
- Other hard-to-define quirky issues that I didn’t see on the tablet – minor stuff that would be annoying long-term


The inability to get a developer license key for Metro style apps was obviously a show-stopper. I know other people who’ve gotten a key on machines joined to a domain, so I doubt that was the issue. My current working theory is that something gets messed up (or got messed up in my case) when upgrading from Win7.

In short, I don’t think I’ll be upgrading from Win7 to Win8 again.

**Fourth**, I did a fresh Win8 install on my laptop. This also went smoothly, though I have some concerns about it automatically getting all the right drivers (like for the motherboard chipset and power control). I guess we’ll see what happens there.

On the whole, running Win8 on a laptop is an adequate experience. The new start screen isn’t as friendly to a mouse as to touch, but it works.

On my tablet and laptop I’ve installed Office 2010 and Lync. These applications appear to work just fine, though they are obviously ill-suited for touch-based usage.

I’ve also installed Visual Studio 11 three times now.

First, I installed it on the tablet. That was a fresh Win8 image, and VS11 installed and ran without a hitch.

Second, I installed it on the upgraded laptop. That was a side-by-side install with an existing VS10 installation. The VS11 install went without a hitch, but as I mentioned earlier, I was unable to get a developer license key for Metro style apps, so it was pretty useless.

Third, I installed it on the reimaged laptop – but after installing VS10 SP1 again. So again, a side-by-side install. The VS11 install went without a hitch, and I’m now happily working on Metro style apps targeting WinRT.
