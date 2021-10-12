---
title: IE8 and the ASP.NET Menu control
postDate: 2009-02-03T09:54:59.9860128-06:00
abstract: 
postStatus: publish
---
03 February 2009

I recently installed the latest version of IE8, bowing to pressure from some of my Microsoft colleagues :)

I don’t regret the decision! IE8 is easily as fast as FF3, and has a lot of really nice, often subtle, features that make it far more useful than IE7.

I was rather excited when I first went to my home page (http://www.lhotka.net), because it rendered correctly. This page renders nice in FF2, FF3 and now IE8. But it never quite worked right in IE7. I was never able to justify the (probably many) hours it would take to troubleshoot the css. Just getting my site working as well as it does was enough to turn my antipathy toward web UI work into tangible dislike.

(I know some people enjoy web UI work. I’ve only found it to be one of the most frustrating experiences in all the years I’ve been programming… Seriously – could we have invented anything more arcane??)

Anyway, my home page renders nicely in IE8, so I’m excited.

Until I try to navigate using one of the drop-down menus. All that appears is a while box! How can IE8 *not render an ASP.NET Menu control?!?!?!?!?!*

Well, it turns out that this is a known issue that the IE8 and ASP.NET teams are working on. It also turns out that it is apparently a z-order issue with the Menu control and the way it renders, so it can be argued that IE8 is actually doing the “right thing” (even though other browsers, including FF3 render the way I’d expect).

In talking to Joshua, Brad and Giorgio at Microsoft a workaround came to light, and Giorgio blogged the [ASP.NET Menu control workaround](http://blogs.msdn.com/giorgio/archive/2009/02/01/asp-net-menu-and-ie8-rendering-white-issue.aspx).

I just had time to try this on my site. I’ll save you the suspense and say that it now does render correctly :)

In my case, I’m using themes and skins, and so I am using a css style to fix the z-order.

To do this, I added the workaround to my site-wide css style sheet:


> .IE8Fix
> {
>     z-index: 1000;
>
> }


And then I edited my skin file to apply this style to all my Menu controls:


> &lt;asp:Menu runat="server" BackColor="#83B8E4"
>
> ...
> **  &lt;DynamicMenuStyle BackColor="#B5C7DE" CssClass="IE8Fix" /&gt;
> ...**
>
> &lt;/asp:Menu&gt;


This was easy for me, because I already had the skin set up to apply numerous other properties and styles to the elements of the Menu control. I simply added the CssClass property to the existing DynamicMenuStyle element.

I published the project to my web server and just like that my Menu control is displaying correctly in IE8.
