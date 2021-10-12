---
title: Things VB can do that C# can't
postDate: 2004-07-14T20:47:07.125-05:00
abstract: A customer asked me for a list of things VB can do that C# can't. "Can't" isn't meaningful of course, but here's a list anyway.
postStatus: publish
---
14 July 2004

A customer asked me for a list of things VB can do that C# can't. "Can't" isn't meaningful of course, since C# can technically do anything, just like VB can technically do anything. Neither language can really do anything that the other can't, because both are bound to .NET itself.

But here's a list of things VB does *easier* or more directly than C#. And yes, I'm fully aware that there's a comparable list of things C# does easier than VB - but that wasn't the question I was asked :-)   I'm also fully aware that this is a partial list.

For the C# product team (if any of you read this), this could also act as my wish list for C#. If C# addressed even the top few issues here I think it would radically improve the language.

Also note that this is for .NET 1.x - things change in .NET 2.0 when VB gets edit-and-continue and the My functionality, and C# gets iterators and anonymous delegates.

Finally, on to the list:
<font size="2"><ol>
<li>One key VB feature is that it eliminates an entire class of runtime error you get in case sensitive languages - where a method parameter and property in the same class have the same name but for case. These problems can only be found through runtime testing, not by the compiler. This is a stupid thing that is solved in VB by avoiding the archaic concept of case sensitivity.
<li>Handle multiple events in single method (superior separation of interface and implementation).
<li>WithEvents is a huge difference in general, since it dramatically simplifies (or even enables) several code generation scenarios.
<li>In VB you can actually tell the difference between inheriting from a base class and implementing an interface. In C# the syntax for both is identical, even though the semantic meaning is very different.
<li>Implement multiple interface items in a single method (superior separation of interface and implementation).
<li>Also, independent naming/scoping of methods that implement an interface method - C# interface implementation is comparable to the sucky way VB6 did it... (superior separation of interface and implementation).
<li>Multiple indexed properties (C# only allows a single indexed property).
<li>Optional parameters (important for Office integration, and general code cleanliness).
<li>Late binding (C# requires manual use of reflection).
<li>There are several COM interop features in VB that require much more work in C#. VB has the ComClass attribute and the CreateObject method for instance.
<li>The Cxxx() methods (such as CDate, CInt, CStr, etc) offer some serious benefits over Convert.xxx. Sometimes performance, but more often increased functionality that takes several lines of C# to achieve.
<li>The VB RTL also includes a bunch of complex financial functions for dealing with interest, etc. In C# you either write them by hand or buy a third-party library (because self-respecting C# devs won't use the VB RTL even if they have to pay for an alternative).
<li>The InputBox method is a simple way to get a string from the user without having to build a custom form.
<li>Sound a Beep in less than a page of code.</li></ol>
<p>And please, no flames. I know C# has a comparable list, and I know I've missed some VB items as well. The point isn't oneupmanship, the point is being able to intelligently and dispassionately evaluate the areas where a given language provides benefit. </p>
<p>If C# adopted some of these ideas, that would be cool. If VB adopted some of C#'s better ideas that would be cool. If they remain separate, but relatively equal that's probably cool too.</p>
<p>Personally, I want to see some of the more advanced SEH features from VAX Basic incorporated into <em>both</em> VB and C#. The DEC guys really had it nailed back in the late 80's!</p>
<p>&nbsp;</p></font>
