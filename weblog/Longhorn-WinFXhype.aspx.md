---
title: Longhorn/WinFX hype
postDate: 2004-02-05T14:20:56.8125-06:00
abstract: Are WinFX and XAML going to provide a common programming model for Windows and the web? Rockford Lhotka doesn't think so.
postStatus: publish
---
05 February 2004

<font size="4"><strong>A</strong></font>fter all the cool WinFX demos at the PDC there's been a lot of speculation about what WinFX and XAML (the XML dialect used to describe forms for WinFX) mean to all of us. One thing I've heard time and time again is that XAML represents a common programming model for Windows and the web.

You can take this concept two ways.

One is to say that there'll be a common model because both web developers and Windows developers will have a cryptic tag language to describe their displays, and will write code behind those tags to drive the UI. And this interpretation appears to be quite accurate - but its not very sexy.

The other is to say that XAML will allow us to write a single client application that can run in either the browser or on a smart client. Somehow the XAML would become HTML for a browser, and would become highly animated Dirext3D code for Windows. I don't buy this view at all, and here's why:

<font size="4"><strong>B</strong></font>ridging the gap in capabilities between the terminal-based browser world and the smart client world is a non-trivial exercise.

I've been thinking for a long time (years) about what must occur for this to be transparent across Windows and Web clients.

On a Windows client all the code behind the form will run right there on the client. Not just the animation stuff, but our UI intelligence and very likely our business logic. In fact, running our business logic (in whole or part) on the client is the whole point of having a smart client, so this point is pretty key. So our UI logic can interact with the full WinFX API. It can also interact with our business objects (or data objects) in a very rich way, since everything is running in a single memory space on the client.

At the same time, we want this to degrade all the way back to a terminal-based browser. In this scheme nothing can run on the client. The client is merely a display vehicle - a colorful 3270 terminal. After all, HTML isn't evolving, so web pages and browser rendering in 2007 will be essentially the same as today (which means the web, or at least HTML, is as good as dead, but that's another topic :-) ).

So where does all our UI code and/or business logic run in the degraded model? It must, by definition, run on the web server. But our code is written to this super-rich WinFX object model, while the user is seeing a dumbed-down terminal representation. In order to fake out our code, the web server will have to give the illusion to our code that it is running within a full-blown client. That way our code can interact with the same objects in the degraded world as it does in the real world.

A web server engine that can translate between a simulated WinFX client (for our UI code) to and from HTML (for the user's terminal) would be really something to see. I very much doubt that something this ambitious is in the works for Longhorn, but it is the only way to provide high-end functionality on Windows with the same code base that could also drive the terminal-based browser experience.

If they went this route, they'd probably need to create at least a couple simulators - one for HTML 3.2 and one for IE 6+ capabilities. Maybe more.

Following this to the extreme, someone could also create a Flash simulator that translated the WinFX reality into something that could be rendered in shockwave. Of course none of our UI code itself could run in shockwave, because our code would still be in .NET assemblies, so the Flash stuff would be pretty lame compared to real Flash work or compare to our actual WinFX UI... Still, it could probably do a limited subset of the WinFX animations, just without any client-side validation or user interaction code.

<font size="4"><strong>S</strong></font>o while a XMAL-&gt;HTML converter could probably be created, that doesn't really solve anything. The real problem is how to make our UI code continue to run when (presumably) the client isn't even running WinFX, or maybe isn't even on the same machine where our UI code is running.
