---
title: Batch processing makes a comeback
postDate: 2017-11-07T14:55:47-06:00
abstract: 
postStatus: publish
---
07 November 2017

When I worked in bio-medical manufacturing batch processing was a core element of our overall IT strategy. Not on the mainframe, but on the VAX.

The OpenVMS operating system, combined with VAX Clusters, had an amazingly powerful and flexible batch processing model, on top of which I wrote a relatively sophisticated scheduling engine to manage our nightly, month-end, and year-end batch processing.

We'd run dozens of batch processes each night, and many more for month/year-end. There were dependencies, and some jobs could or couldn't run in parallel with other jobs. My scheduler managed all that automatically, allowing users to add/remove requests for processing jobs and ensuing they fit into the schedule appropriately.

That basic robust batch processing capability is something I've missed ever since coming to Windows (so for 20+ years now), and I'm really thrilled to see the feature available as a first-class offering in Azure.

The fact that [Azure also provides low-priority/lower-cost batch hosts](https://blogs.msdn.microsoft.com/uk_faculty_connection/2017/11/07/microsoft-azure-low-priority-virtual-machines-take-advantage-of-surplus-capacity-in-azure/) is a nice bonus.

Now people are going to have to dig back in their memories, or start from scratch, and learn how to fully leverage batch processing once again!
