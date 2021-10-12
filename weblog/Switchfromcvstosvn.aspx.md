---
title: Switch from cvs to svn
postDate: 2007-01-30T12:43:13.774-06:00
abstract: 
postStatus: publish
---
30 January 2007

Thanks to a lot of work by fellow [Magenic](http://www.magenic.com) consultant Chuck Macomber, my CSLA .NET code is now in Subversion (svn) rather than in cvs. Thank you Chuck!!

I'm told that svn offers many advantages over cvs. Just at the moment all I see are the differences where I need to learn and adjust, but that will pass :)

I've left cvs alive for the moment, but Chuck was able to port all the history into svn, so once things get settled I should be able to entirely drop cvs.

The svn repository is at svn://svn.lhotka.net/csla, and it should be open for anonymous read. As with cvs, I'm allowing anyone to read the contents of the respository.

Also, the web viewer (http://www.lhotka.net/cslacvs) remains alive, but now defaults to using the svn repository. The cvs repository is still visible there too, just use the drop-down in the upper right-hand corner of the page to switch to it. <strike>One known issue at this time, is that the diff function doesn't work in svn. I don't know why, but python seems unable to find the diff program under svn, though it works fine under cvs.</strike>

<strike>If you have any idea how to solve this diff issue, I'm all ears. Google, thus far, has been of little value... </strike>(I am now guessing the diff issue was a caching problem, because it simply started working all by itself... Gotta love web development...)

Going forward, all changes to CSLA .NET will occur in the svn repository.
