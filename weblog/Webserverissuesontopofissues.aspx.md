---
title: Web server issues, on top of issues
postDate: 2008-03-14T19:35:51.0722192-05:00
abstract: 
postStatus: publish
---
14 March 2008

Sometimes you just can't catch a break...

About two weeks ago my server's motherboard went bad. That's no fun, but http://www.lhotka.net is running in a virtual machine (VM) on Virtual Server, so it was relatively easy to get it back running on my desktop workstation. Not ideal, but a temporary workaround. And since I was heading to Las Vegas for MIX 08 I didn't need the desktop anyway.

Last weekend my good friend (and hardware guru) Rick came over and we confirmed it was the motherboard, and purchased replacement parts. A shiny new Q6600 CPU and a motherboard to match. Now my physical server is a quad core machine, and that's very cool. Though I am running Windows Server 2003 64 bit and Virtual Server 2005 R2 as the host, so the VM still can't use more than one CPU :(  Still, each core of the new CPU is much faster than the previous single-core CPU.

On Monday I got the VM copied off my desktop and onto the new server. All seemed to be working, which made me happy. And I blissfully flew off to LA to spend the week with a client.

Only to find out that there's a problem! The VM uses a virtual network adapter that is attached to the host's real network adapter. For some reason the VM periodically sees the network adapter become "unplugged". Which of course it is not. The physical NIC is working fine, but the VM is losing it. Manually disabling/enabling the virtual NIC fixes the problem, but this happens every few hours (so if you've noticed http://www.lhotka.net offline a lot the past few days this is why).

Also, my System event log was (and is) filling up with "The netcard driver failed the query for OID\_GEN\_LINK\_SPEED", related to the QoS service.

Googling turned up a few people who've had the same problem. But no serious answers. Apparently people solved the problem but never posted their solution in any coherent manner. More googling, and then more... Eventually I found some tidbits of info here and there. Things to try:

1. Disable the QoS service on the virtual NIC (had no effect for the original poster or me - though it does stop the event log entries)
2. Remove the virtual NIC and restart the VM so it redetects the NIC (didn't work for the original poster, nor for me)
3. On the host, uncheck the virtual server support on the real NIC, reboot the host, re-check the virtual server support on the real NIC, reboot the host (I don't know if it helped the original poster, but it didn't help me)
4. I noticed that the host didn't have the Windows Firewall turned on, so today I turned it on (I don't know yet if that had any impact, but I feel better having done it)
5. Uninstall Virtual Server, then reinstall it (don't know if it worked for the original poster, and haven't tried this yet)


Interestingly enough, enabling the firewall on the host *might* have had an impact. The VM has been successfully running for around 5 hours now. I am rather doubtful that this is the problem, but maybe I'll get lucky. I still can't enable the QoS service without flooding the event log with errors though...

To add insult to injury, as I was messing with all this today (running on 3 hours of sleep and having just flown back from LA), some spammer decided to target my wife's blog for pingback spam. It is like a denial of service attack - they are sending 4-5 post requests to her blog every second. And dasBlog is clearly not capable of handling that kind of volume. So the VM pegs at 100% CPU, the disk is thrashing, everything is incredibly slow, and they somehow got past the fact that she has pingbacks turned *off* and managed to load hundreds of them into her blog...

The dasBlog cleaner utility got rid of about 70% of them, and I wrote a quick VB app to clean the rest (the LINQ to XML support in VB is so *incredibly awesome!!!*), and we tweaked some more settings so I don't think they can get the pingbacks to record anymore. But they are still trying, so now it really is a DOS attack.

Do I think spammers should go to prison? Absolutely. They cause direct, tangible harm, and they should be deprived of their ability to harm or interact with normal human beings if at all possible. They are like mass muggers.

What puzzles me is that the URLs they were spamming into the blog don't actually go anywhere. Each one was unique and semi-random. I can't figure out the motivation behind this, since they clearly can't get any value out of a URL that doesn't go anywhere can they?

So maybe they shouldn't to prison. Maybe they should be locked up in a looney bin somewhere?

Anyway, I very much doubt this is the end of the saga. Though I think I've blocked the pingbacks, they continue to pound the server. And I expect the server's NIC to disconnect any time now - in which case I'll try the uninstall/reinstall of Virtual Server in the hope that solves the problem...

I really, really hate computers sometimes...
