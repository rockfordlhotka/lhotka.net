---
title: How to sync an HP IPAQ 4150 with Windows Vista
postDate: 2007-05-29T09:46:32.4755568-05:00
abstract: A tale of frustration and woe - but with a happy ending, thanks to help from some most excellent colleagues!
postStatus: publish
---
29 May 2007

<font face="Calibri" color="#000000" size="3">I post this in the hopes that it will help prevent someone else’s pain. And because the search engines (live and google) never did give me any of these answers – they are totally clogged up with content from pre-release versions of Vista and with sites trying to sell or review mobile devices…</font>

<font face="Calibri" color="#000000" size="3">My wife has an HP 4150 – a wonderful little PDA. And a while back I put Vista on her laptop. Yesterday she tried to get it to sync, but Vista wouldn’t recognize the device. So she asked me for help, and there begins my tale of woe.</font>

<font face="Calibri" color="#000000" size="3">She was right, Vista would see the device through Explorer, so you could copy files back and forth, but the Windows Mobile Device Center (WMDC) wouldn’t see it at all.</font>

<font face="Calibri" color="#000000" size="3">After much time googling (see above) I gave up and went directly to the WMDC site – their home page never did show up in google (or live.com)… They say clearly that Windows Mobile 2003 is supported, and the HP 4150 clearly runs WM2003.</font>

<font face="Calibri" color="#000000" size="3">So now I’m perplexed. What could be wrong? Ahh! Perhaps there’s an update to the device from HP.</font>

<font face="Calibri" color="#000000" size="3">Go to hp.com and sure enough, there’s a ROM upgrade, which I downloaded.</font>

<font face="Calibri" color="#000000" size="3">By this point it was a little late, and I was a little frustrated that something so simple and obvious could be so hard. And the Microsoft page made no mention of any difficulties or challenges. No help with troubleshooting – or even any indication that troubleshooting would be required.</font>

<font face="Calibri" color="#000000" size="3">So I ran the ROM upgrade utility. On the Vista box. Stupid me. It started, and then failed. Leaving the IPAQ in a totally locked state. As long as the battery was in the device (I took the batter out a few times trying to reset things), the device was on a white logo screen showing a couple numbers (which I assume are hardware revision numbers or something).</font>

<font face="Calibri" color="#000000" size="3">At this point I appear to have a battery-powered paperweight, where once I had a PDA. Damn!</font>

<font face="Calibri" color="#000000" size="3">That was last night. Fortunately I have some awesome colleagues, and a couple of them replied to my email rant (I wasn’t happy).</font>

<font face="Calibri" color="#000000" size="3">Overnight I had left the battery out of the device. It apparently takes a few hours for some capacitors to discharge, and so at a colleague’s suggestion I put the battery back in this morning. Much to my relief the device rebooted with factory settings. Whew!</font>

<font face="Calibri" color="#000000" size="3">Then, following the suggestion from a Microsoft colleague, I ran the ROM upgrade from an XP machine. While the ROM upgrade utility will try to run on Vista, it won’t succeed – bad HP for not including an OS version check in such a critical utility!! One simple check like that would have saved me substantial trouble!</font>

<font face="Calibri" color="#000000" size="3">The upgrade works great from XP. Which is a lesson: if you decide to upgrade to Vista, make sure to keep at least one XP machine around for the next year or so, until these issues get ironed out. (A corollary to this is that if you only have one machine, you probably won’t want to go to Vista…)</font>

<font size="3"><font face="Calibri"><font color="#000000">It turns out however, that the ROM upgrade didn’t fix the sync issue. This is because Vista didn’t ship with the release version of WMDC. To get the release version of WMDC 6, you need to go to </font><span style="COLOR: #1f497d"><a href="http://www.microsoft.com/windowsmobile/devicecenter.mspx"><font color="#800080">http://www.microsoft.com/windowsmobile/devicecenter.mspx</font></a> </span><font color="#000000"><span style="mso-spacerun: yes">&nbsp;</span>and download the current version. </font></font></font>

<font face="Calibri" color="#000000" size="3">In theory I guess Windows Update is supposed to update WMDC for you, but in my experience that’s not true. I had to do force the upgrade manually.</font>

<font face="Calibri" color="#000000" size="3">Also, I still don’t know how to find out the version of WMDC you have installed on a machine. So I guess you could argue that everyone should go run that update just in case.</font>

<font face="Calibri" color="#000000" size="3">So let me recap. I did the following:</font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Tried to sync a WM2003 device with Vista (a supported activity, with no indication that there are issues from Microsoft’s web site) – this failed</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Tried to do a ROM upgrade of the HP 4150 from Vista – this failed horribly</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Found out that the device would reboot after a few hours without power (thankfully!)</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Did the ROM upgrade from XP – successfully</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Manually upgraded WMDC on Vista</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Got the device to sync with Vista</font></font>

<font face="Calibri" color="#000000" size="3">Now my wife has a PDA again, which makes her happy. And that, of course, makes me happy.</font>

<font face="Calibri" color="#000000" size="3">And with any luck, this post will appear within the first few pages of a search about how to sync an HP IPAQ 4100 series (HP 4150) with Windows Vista through the Windows Mobile Device Center, and so can save someone else all the time and effort this process cost me…</font>
