---
title: My Vista Experience (thus far)
postDate: 2008-05-30T11:45:18.0531952-05:00
abstract: 
postStatus: publish
---
30 May 2008

I have hesitated to publicly discuss my experiences with Vista, acting under the theory that if you can't say something nice you shouldn't say anything at all. But at this point I have some nice things to say (though not all nice), and I think there's some value in sharing my experiences and thoughts.

On the whole, my experience with Vista has been decidedly mixed.

Vista is very pretty. It is clearly the future in many ways (especially around IIS 7 and WAS and security in general). And it has some nice usability features – like a far better replacement for ntbackup, and pre-enabled shadowing (so you can retrieve old files if you lose/overwrite them). And quite a few OS features are easier to find/use than in XP (once you get used to the changes).

However, it is slower and more resource-intensive than XP. So you can’t upgrade from XP and expect the same level of performance or responsiveness on the same hardware. If your hardware is more than a few months old, I really can't recommend an upgrade.

I upgraded my (now 2 year old) laptop when Vista came out, and have been generally displeased with the results. It is running Vista Business. However, as Vista has aged Microsoft has issued patches/fixes/updates that have helped with stability and performance. I would say that it is now tolerable, or at least I’ve learned to live with it. While it is workable, it isn't really satisfying - to me at least. My laptop is a dual core machine with 3 gigs of RAM and a low-end GPU.

One thing I'll note is that upgrading the laptop from 2 to 3 gigs of RAM made a *huge* difference in performance. Vista really likes memory, and the more you can get in your machine the happier you'll be.

I didn’t upgrade my desktop to Vista until I replaced my desktop machine. I do almost all my work on this machine, and wasn't about to deal with the performance issues on a constant basis.

My new desktop machine, which is running Vista Ultimate, is a quad core with 4 gigs of RAM and a high end GPU. I find that Vista runs quite adequately on this (admittedly high-end) machine. My current bottlenecks are memory speed (but DDR3 is too expensive) and disk IO (but 10k RPM disks are too loud – I’m one of those “silent computer” nuts).

I have colleagues who are running Vista 64 bit. Apparently that is faster and more stable (partially due to fewer iffy drivers, and because 64 bit gets *all* your 4+ gigs of RAM). But I'm a gamer, so I'm kind of stuck with 32 bit until there are 64 bit versions of Battlefield 2142, Supreme Commander, Sim City 4 and Civ IV :)

One thing that has really helped my Vista experience is the discovery of [TeraCopy](http://www.codesector.com/teracopy.php). Vista is notorious for slow file copies (especially when copying multiple files). It is a bit sad that Vista's slow file copies have enabled a product niche for something like a file copy utility (how 1990 is that!), but whatever, it works.

I have UAC turned on. I realize many devs turn it off. But if our users are to live with it, I think developers should too. And personally I think it should be illegal for Microsoft employees to turn it off – they should know what they are doing to their customers.

The thing is, I have not found UAC to be overly troublesome. Yes, there are some extra dialogs when installing software – but that’s not a big deal imo, and is an acceptable trade-off for the security. The bigger frustration with UAC are simpler things like trying to create a favorite in IE, or copy a shortcut to the Programs menu – both of which turn out to be really hard due to UAC.

I have done some work with VS 2005 under Vista. You have to run as admin to debug web apps, which means you can't double-click sln files. There may have been some other quirks too, I don't recall. Long ago I created a virtual machine with XP where I have VS 2005 installed, and any 2005 work is done there (for .NET 2.0/3.0 - primarily maintenance for CSLA .NET 3.0).

For months now I've been using VS 2008, largely under Vista. The experience is quite smooth. You do have to run 2008 as admin to debug a web app running in IIS, but not in the dev web server. It really isn’t a big deal to run as admin for VS if you need to debug a web app. This is the intended “escape hatch” for developers that need to do things a normal user should not be able to do. It is a little frustrating to not be able to double-click a sln file, but I can deal with that small issue.

And for WPF or Windows Forms work (and a lot of web work where the dev server can be used) then you don't need to run as admin at all.

In the final analysis, if you have a relatively new machine with high-end hardware and lots of RAM, then I think Vista is a fine OS, even for a developer. But if your machine is more than a few months old, has less than 3 gigs of RAM or has an older GPU, I'd hesitate to leave XP.
