---
title: New web site
postDate: 2006-07-11T13:31:12.220016-05:00
abstract: Trials, tribulations and choices of the upgrading process
postStatus: publish
---
11 July 2006

After spending (what to me was) an unbelievable number of hours fighting with css, I have a new web site: [www.lhotka.net](http://www.lhotka.net/) is now ASP.NET 2.0, with master pages, themes and a pure css layout. Special thanks to Mike Gale for helping me with some issues, and to http://www.positioniseverything.net/ for providing tools that generate various types of css layouts. It continues to amaze me that you need a tool (and various browser-specific hacks) to generate simple tabular page layouts - but I guess that's the web for you...<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

Anyway, the end result is that the web site is no longer hosted on a ~7 year old dual P3/450 machine with 512 megs of RAM - but rather is hosted on a (relatively) new Athalon 3100 with a couple gigs of RAM. So not only does it look different, but it is a bit faster too :)<o:p></o:p>

However, some of the speed is bled off by my choice to jump into virtualization. The web "server" is actually now a virtual machine. (yes, I know you are supposed to keep these sorts of details private to slow hackers - but sharing information is the key to forward motion...) <o:p></o:p>

I chose to do this because it means I have a lot more flexibility going forward. In particular, if this physical machine were to crash, I could rehost the vhd files on another machine and get running again relatively fast. Trying to do that with an OS directly installed on the hard drive is non-trivial (requiring something like Ghost or Acronis TrueImage).<o:p></o:p>

With the virtualization, I can script it so the VM shuts down, the vhd files are copied elsewhere (as a backup) and the VM is restarted. Full image backups in just a couple minutes! Hard to beat that as a feature!<o:p></o:p>

It is also the case that this server box is largely underutilized. It isn’t like my web site or blog are popular enough to overwhelm the machine. So now I have the ability to host other virtual machines on the same physical box, for testing of beta software or hosting other types of servers if I have the need going forward.<o:p></o:p>

I had also considered moving from cvs to svn at the same time as the rest of the upgrade process. In researching that, I decided there was simply too much risk. While Subversion installed OK, the cvs2svn tool was unable to handle the CSLA .NET code repository. As with many of these tools, it was written by Un\*x people for their needs, and has never really be made to work with the Windows equivalent software (cvsnt in my case). While it works for some people, my repository is apparently too old and complex (tagging/branching/deleting of files/directories).<o:p></o:p>

The end result is that switching to svn means abandoning all the history I have in cvs. I’m not quite ready to do that, nor do I want to lose the cvsgraph abilities from viewcv (because there’s no equivalent for svn at present I guess). So for now, at least, I’m sticking with cvs.<o:p></o:p>

Of course the *obvious* question is why I didn’t switch to Microsoft VSTS/TFS. There are perhaps two good reasons: licensing and functionality. Licensing isn’t a problem for me directly – I have a workgroup license that would serve me fine. But it isn’t clear that I could expose the code repository externally and still satisfy the license – and I think there’s tremendous value in http://www.lhotka.net/cslacvs... And functionality is an issue too – primarily in that I don’t know of a viewcv equivalent for TFS. So even if licensing is/was a non-issue – the lack of a read-only web viewer for the repository is a show-stopper.<o:p></o:p>

Given time I am sure these issues will work themselves out – so by the time I’m ready to move off cvs perhaps TFS will be a viable choice alongside Subversion. Time will tell…<o:p></o:p>
