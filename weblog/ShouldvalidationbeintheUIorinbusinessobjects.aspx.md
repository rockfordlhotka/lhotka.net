---
title: Should validation be in the UI or in business objects
postDate: 2006-03-01T15:44:33.093-06:00
abstract: You probably already know my conclusion - but the article is probably worth reading anyway :)
postStatus: publish
---
01 March 2006

<font size="3"><font color="#000000"><font face="Times New Roman">I was recently asked whether I thought it was a good idea to avoid using the Validation events provided by Microsoft (in the UI), in favor of putting the validation logic into a set of objects. I think the answer to the question (to some degree) depends on whether you are doing Windows or Web development.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">With Windows development, Windows Forms provides all the plumbing you need to put all your validation in the business objects and still have a very rich, expressive UI - with virtually no code in the UI at all. This is particularly true in .NET 2.0, but is quite workable in .NET 1.1 as well.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">With Web development life isn't as nice. Of course there's no way to run real code in the browser, so you are stuck with JavaScript. While the <i style="mso-bidi-font-style: normal">real</i> authority for any and all business logic <i style="mso-bidi-font-style: normal">must</i> reside on the web server (because browsers are easily compromised), many web applications duplicate validation into the browser to give the user a better experience. While this is expensive and unfortunate, it is life in the world of the Web.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">(Of course what <i style="mso-bidi-font-style: normal">really</i> happens with a lot of Web apps is that the validation is <b style="mso-bidi-font-weight: normal">only</b> put into the browser - which is horrible, because it is too easy to bypass. That is simply a flawed approach to development...)<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">At least with ASP.NET there are the validation controls, which simplify the process of creating and maintaining the duplicate validation logic in the browser. You are still left to manually keep the logic in sync, but at least it doesn't require hand-coding JavaScript in most cases.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Obviously Windows Forms is an older and more mature technology (or at least flows from an older family of technologies), so it is no surprise that it allows you to do more things with less effort. But in most cases the effort to create Web Forms interfaces isn't bad either.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">In any case, I do focus greatly on keeping code out of the UI. There's nothing more expensive than a line of code in the UI - because you _know_ it has a half-life of about 1-2 years. Everyone is rewriting their ASP.NET 1.0 UI code to ASP.NET 2.0. Everyone is tweaking their Windows Forms 1.0 code for 2.0. And all of it is junk when WinFX comes out, since WPF is intended to replace both Windows and Web UI development in most cases. Thus code in the UI is expensive, because you'll need to rewrite it in less than 2 years in most cases.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Code in a business object, on the other hand, is far less expensive because most business processes don't change nearly as fast as the UI technologies provided by our vendors... As long as your business objects conform to the basic platform interfaces for data binding, they tend to flow forward from one UI technology to the next. For instance, WPF uses the same interfaces as Windows Forms, so reusing the <i style="mso-bidi-font-style: normal">same</i> objects from Windows Forms behind WPF turns out to be pretty painless. You just redesign the UI and away you go. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">A co-worker at </font>[<font face="Times New Roman" size="3">Magenic</font>](http://www.magenic.com/)<font face="Times New Roman" color="#000000" size="3"> has already taken my ProjectTracker20 sample app and created a WPF interface for it – based on the same set of CSLA .NET 2.0 business objects as the Windows Forms and Web Forms interfaces. Very cool!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So ultimately, I strongly believe that validation (and all other business logic) should be done in a set of business objects. That’s much of the focus in my upcoming </font>[<font face="Times New Roman" size="3">Expert VB 2005 and C# 2005 Business Objects</font>](http://www.lhotka.net/cslanet/csla20.aspx)<font face="Times New Roman" color="#000000" size="3"> books. While you might opt to duplicate some of the validation in the UI for a rich user experience, that’s merely an unfortunate side-effect of the immature (and stagnant) state of the HTML world.</font>
