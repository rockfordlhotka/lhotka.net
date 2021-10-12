---
title: When Windows Home Server crashes&hellip;
postDate: 2009-06-26T16:37:24.6042766-05:00
abstract: 
postStatus: publish
---
26 June 2009

I’ve had quite the experience over the past couple weeks.

Three weeks ago I was in Las Vegas speaking at [VS Live](http://www.vslive.com). While there, I realized I’d forgotten to copy some key files to my laptop before leaving home, but Windows Home Server made that a non-issue, since it provides a secure web interface to my files. Awesome!

Then I got home and discovered that one of the two additional hard drives I added to my WHS machine was failing. This was unpleasant, but not cause for alarm since all my key files are set to duplicate.

(I only discovered the failure because WHS started crashing, and I looked in the Windows system event log to find the drive failure notifications – they’d been occurring for several days, but I don’t check my system event log daily, so I didn’t know – this is the one place where WHS really let me down – I still don’t know why Windows knew the drives were going to fail, but WHS blindly ignored this clear intelligence…)

Unfortunately I couldn’t get WHS to dismount (remove) the failing hard drive. After 3-4 tries, it finally did remove the drive. This took 2.5 days, since each failure took 12-24 hours, as did the final success.

I should also note that I was under serious time pressure, because I was flying out to Norway for the NDC conference and only had about 3.5 days to solve the problem!

After the failed drive was removed, things were obviously not right on the WHS machine. Clearly the remove didn’t work right or something. Poking around a bit further, I found that the *second additional hard drive was also failing*. What are the odds of two drives failing at once? Small, but yet there I was.

I quickly bought and installed a brand new hard drive (Seagate this time, since the dual failures were Western Digitals) and tried to remove the second failing drive. The attempt was still running when I flew to Norway.

Fortunately Live Mesh allowed me to use remote desktop to get back into my network, and I kept trying to remove the drive (failure after failure) while in Norway.

When I returned from Norway I manually removed the drive. Clearly it wasn’t going to remove through software. I can’t say this made matters worse, but it sure didn’t make them better either. Now WHS *still wouldn’t remove the drive* even though it was shown as “missing”. It had “locked files” and couldn’t be removed.

Thanks to some excellent help from the Microsoft WHS forum (thanks Ken!) I came to realize that my only option at this point was to repair the WHS OS – basically do a reinstall. I have the cute little HP appliance, and it comes with a server restore disk – pop it into my desktop machine, run the wizard and in very little time I had my server back, just like when I bought it originally.

OK, so now I have a functioning WHS again, but it is empty, blank – all my data is gone!

I’ve been here before (a couple times) with other servers though, so I have backups for my backups. All “critical” data is always in 3 places. So I just restored my server backup and got back my “critical” files – everything for my work, all the family photos and home videos of the kids, etc.

Here’s the catch though – I rapidly discovered that my “non-critical” data is actually pretty critical. Things like music, videos and miscellaneous files.

The music I was able to recover from a Zune device. I tried *my* Zune device, but that was a mistake. As soon as I connected it to my desktop machine it synced – and it discovered I’d “deleted” all my music and so it cleared the device. Damn!

Fortunately my son also has a fully-synced Zune, and I connected his to my desktop machine as a guest. No automatic sync, and so I was able to highlight all music on his device and say “copy to my collection”. Just like that all our music was back on the server.

I still don’t have any videos or miscellaneous files. They are gone. Arguably this isn’t the end of the world, as technically I can get back anything that really matters – by re-downloading, or getting files from friends, etc. But that’s all a pain in the butt and a waste of time, so it is unfortunate.

(it might be that I can recover some of them from the two defunct hard drives – using various data recovery tools I may be able to connect them to my desktop machine and retrieve some of the files – but that’s also a big hassle and may not be worth the effort)

So what did I learn out of all this?

1. WHS is awesome, and I still really love it
2. WHS can’t handle two hard drives failing at once – if that happens you better have a backup for your server
3. “Critical” files include things that aren’t *really* critical like music and maybe videos – external hard drives to backup the server are relatively cheap – just get a 2 TB external drive and back up everything – that’s my new motto!


Oh, and I’m now using IDrive to get offsite backups for my *truly critical* files. I know, I didn’t need it in this case, but the whole experience got me thinking about floods, tornadoes, fire, etc. What if I did lose my family photos or home videos? The last 15 years of my life is digital, and nearly all record would be lost in such a case. Having automatic backups of that data, along with other important documents and files seems really wise.

So now my super-critical files are in at least 4 places (one offsite). My critical files (using my newly expanded definition) are in at least 3 places. And my non-critical files are in 2 places. I’m so redundant I’m starting to feel like NASA :)
