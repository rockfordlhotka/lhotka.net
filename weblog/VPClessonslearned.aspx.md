---
title: VPC lessons learned
postDate: 2005-06-06T15:26:36.546875-05:00
abstract: Tips and tweaks to make VPC run smoother and faster
postStatus: publish
---
06 June 2005

Virtual PC (and/or Visual Server) are the most wonderful things to happen in a long time - especially if you use any beta software or do any system configurations that might damage or corrupt a real system.

But getting these things to run fast, especially on a laptop, can be a serious challenge. Here's a checklist of things I've been doing recently to get decent performance.

1. Make sure to uninstall/reinstall VPC and SP1 after upgrading the host Windows XP to SP2
2. Make sure to install/reinstall the VPC add-in software on the guest OS after upgraded to VPC SP1
3. Put your vhd and vmc files on different physical hard drives (not just partition)
4. If possible, put your vhd files on a different physical hard drive (not just partition) from your host OS system drive
5. Before starting VPC, do the following on the host
    1. Stop SQL Server
    2. Stop IIS
    3. Stop any virus scanning software
    4. Stop Messenger or other IM software
    5. Close all apps
    6. Close or stop any other items in the system tray or via the Services manager - anything you can stop that doesn't crash the host is to your benefit
6. Grant your VPC the most memory you can afford. After doing step 3, I'm able to grant 640 meg to the VPC on a 1 gig host machine.
7. The more memory on the host machine the better. 2+ gigs of RAM rocks!
8. If you need to put the host in standby, close VPC *entirely* first. Not just VPC instances, but close the VPC console itself. There are bugs with VPC that cause display failure issues when the host comes out of standby
9. If your VPC mouse pointer ends up with a black box around it (in LiveMeeting or other projection software), go to your video settings under the Settings tab, Advanced button and turn hardware acceleration down one notch


I'm sure there are other tips and tweaks, but doing these helps a whole lot with VPC happiness!


