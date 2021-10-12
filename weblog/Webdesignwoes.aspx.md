---
title: Web design woes
postDate: 2006-06-25T13:52:10.125-05:00
abstract: 
postStatus: publish
---
25 June 2006

I've never pretended to be a UI expert - especially not for the web. (I am very good at designing heads-down data entry screens that minimize keystrokes and avoid the use of the mouse - but that's far from being good at making things pretty)

So I'm trying to create an updated version of http://www.lhotka.net. To do this I'm using ASP.NET 2.0 master pages, and avoiding all use of tables - only div statements are allowed. This way I can use ASP.NET 2.0 theme/skin support to get the appearance (working with the div layout in the master page). And it looks pretty good in IE too. After a *lot* of time figuring out how css works - and how it cascades settings from one level down to the next - it finally looks pretty decent.

So then I open it in Firefox. Apparently FF doesn't follow the same rules *at all*. Settings don't cascade from one div to a lower div. Settings like height: 100% apparently are ignored entirely. And my content area refuses to sit beside the nav area, and when I manage to get them sitting side-by-side the width is different from the header - since the width apparently didn't cascade from the top-level div tag's style.

No wonder web development is so damn expensive. Doing something simple like laying out a standard page with header/nav/body is apparently radically different between IE and FF. Worse yet, FF must use a totally different mental model... Where Bill Clinton wanted to know the meaning of "is", it appears that FF needs to know the meaning of "cascade"...
