---
title: Post-PDC networking blues
postDate: 2005-09-19T15:01:36.640625-05:00
abstract: 
postStatus: publish
---
19 September 2005

Upon returning from the Microsoft PDC conference I found that my laptop could no longer access the nodes on my LAN. I could ping machines by IP address, but local name resolution was not working. After much discussion and running many network commands as suggested by various colleagues, my co-workers at [Magenic](http://www.magenic.com)hit upon the answer.

Apparently it is possible for your machine's network node type to be switched by any DHCP server. My DHCP server doesn't set the node type at all, but the one at PDC apparently set it to Peer-to-Peer, which I'm told forces your machine to only use a WINS server for name resolution on a LAN. I don't have a WINS server, so all name resolution was shot to hell when I got back from PDC.

The solution was to change my node type from Peer-to-Peer to almost any other value: b-node, Hybrid or Unknown are all good. Since there's no end user tool to do this, regedit is your friend as noted in [this blog entry](http://www.h2co3.com/blog/archives/000011.html).

Situations like these remind me why I'm a software and not an infrastructure person. I find troubleshooting and solving this stuff to be frustrating and not at all fun... It is probably an aftertaste from my brief stint (18 months or so) of managing a corporate help desk many years ago - because that wasn't at all fun either.
