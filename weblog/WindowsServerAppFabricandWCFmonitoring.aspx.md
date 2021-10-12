---
title: Windows Server AppFabric and WCF monitoring
postDate: 2011-03-22T10:13:40.0703698-05:00
abstract: 
postStatus: publish
---
22 March 2011

Yesterday I set out to do “something simple” – to use Windows Server AppFabric to do basic health monitoring of a WCF service.

A few hours later, I was pulling my hair out and my brain was spinning.

The basic issue is that configuring and using AppFabric involves numerous moving parts, and that leads to a ton of complexity for something that is otherwise pretty simple. But there are a lot of moving parts:

1. My app
2. IIS
3. ASP.NET
4. WCF
5. AppFabric configuration tool
6. AppFabric Dashboard
7. AppFabric event collection service
8. SQL Server
9. SQL Server Agent
10. Machine.config
11. Web.config
12. Visual Studio
13. NTFS security


To make matters worse, on my dev workstation I had SQL Express 2005, SQL Express 2008 R2, and SQL Server 2008.

What you are *supposed* to do is simply this:

1. install your web site into IIS (create an IIS Application where the virtual root points to your web site directory)
2. in IIS Manager go to the virtual root, and click the Configure link on the far right under the Manage WCF and WF Services label
3. in the resulting dialog, click Monitoring on the left, then enable application monitoring
4. call your service
5. back in IIS Manager, double-click the AppFabric Dashboard option for your virtual root to see the dashboard, with the cute little counters showing that your services have been used


Of course that didn’t work.

In the end, I *think* it didn’t work because the AppFabric Event Collection Service (a Windows service that runs to collect event information) didn’t have NTFS security rights to read my application’s web.config file.

But that’s not the first thing I thought to check. No, the first thing I thought to check was whether data was getting into the AppFabric tables in SQL Server. It was not. So then (after a little googling with Bing), it sounded like the problem was that SQL Agent wasn’t running.

Of course it turns out that SQL Agent can’t run against SQL Express. But having three different versions of SQL Server installed was making this all very hard to troubleshoot. So I spent some quality time uninstalling SQL 2005 and 2008, and then installing SQL Server Developer 2008 R2 – so now I have a real up-to-date SQL Server instance where SQL Agent does work.

(again, I suspect that was all wasted time – but on the upside, I have a far less confusing SQL Server installation ![Smile](binary/Windows-Live-Writer/Windows-Server-AppFabric-and-WCF-monitor_8BCD/wlEmoticon-smile_2.png) )

All that work, and it didn’t help. Then it occurred to me that my configurations were probably out of sync. So I reconfigured AppFabric, and my app, and the web sites and virtual roots in IIS Manager – all to use the new 2008 R2 database. And things were out of sync, so this was necessary and good.

But that didn’t help either. Still no data was in the AppFabric database.

Finally, I found a [page lurking deep in MSDN](http://msdn.microsoft.com/en-us/library/ee677384.aspx) that contained good troubleshooting information. And in here were instructions on how to view the event log for the AppFabric event collection service – which couldn’t read my web.config file.

I thought I’d hit the jackpot, so I updated the NTFS permissions on my web folder so the collection service could read the directory.

Still nothing. So I went to bed, frustrated at the continual failure.

This morning I thought I’d try again. Still no joy. So I rebooted my machine, and then it worked.

So I suspect that the core issue was the NTFS file permissions for the collection service. But with all the other changes I made, some service didn’t re-read its configuration until the system was rebooted.

In the end, it only took me about 6 hours of work to get Windows Server AppFabric to monitor the health of my WCF service. Hopefully I’ll never have to go through that again…
