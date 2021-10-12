---
title: Where Workflow Foundation really shines
postDate: 2006-09-05T12:24:24.056344-05:00
abstract: Depending on who you talk to, WF should be used to do almost anything and everything. It can drive your UI, replace your business layer, orchestrate your processes and workflow, manage your data access and solve world hunger... My view on WF is a bit more modest.
postStatus: publish
---
05 September 2006

<font face="Times New Roman" color="#000000" size="3">Several people have asked me about my thoughts on the Microsoft .NET 3.0 Workflow Foundation (WF) technology.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">My views certainly don’t correspond with Microsoft's official line. But the “official line” comes from the WF marketing team, and they'll tell you that WF is the be-all-and-end-all, and that's obviously silly. Microsoft product teams are always excited about their work, which is good and makes sense. We all just need to apply an "excitement filter" to anything they say, bring it back to reality and decide what really works for us. ;)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Depending on who you talk to, WF should be used to do almost anything and everything. It can drive your UI, replace your business layer, orchestrate your processes and workflow, manage your data access and solve world hunger…</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">My view on WF is a bit more modest: </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Most applications have a lot of highly interactive processes - where users edit, view and otherwise interact with the system. These applications almost always also have some non-interactive processes - where the user initiates an action, but then a sequence of steps are followed without the user's input, and typically without even telling the user about each step.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Think about an inventory system. There's lots of interaction as the user adds products, updates quantities, moves inventory around, changes cost/price data, etc. Then there's almost always a point at which a "pick list" gets generated so someone can go into the warehouse and actually get the stuff so it can be shipped or used or whatever. Generating a pick list is a non-trivial task, because it requires looking at demand (orders, etc.), evaluating what products to get, where they are and ordering the list to make the best use of the stock floor personnel's time. This is a non-interactive process.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Today we all write these non-interactive processes in code. Maybe with a set of objects working in concert, but more often as a linear or procedural set of code. If a change is needed to the process, we have to alter the code itself, possibly introducing unintended side-effects, because there's little isolation between steps.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Personally I think this is where WF fits in. It is really good at helping you create and manage non-interactive processes.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Yes, you have to think about those non-interactive processes in a different way to use WF. But it is probably worth it, because in the end you'll have divided each process into a set of discrete, autonomous steps. WF itself will invoke each step in order, and you have the pleasure (seriously!) of creating each step as an independent unit of code. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">From an OO design perspective it is almost perfect, because each step is a use case, that can be designed and implemented in isolation - which is a rare and exciting thing!<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Note that getting to this point really does require rethinking of the non-interactive process. You have to break the process down into a set of discrete steps, ensuring that each step has very clearly defined inputs and outputs, and the implementation of each step must arbitrarily ensure any prerequisites are met, because it can't know in what order things will eventually occur.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">The great thing (?) about this design process is that the decomposition necessary to pull it off is exactly the same stuff universities were teaching 25 years ago to COBOL and FORTRAN students. This is procedural programming "done right". To me though, the cool think is that each "procedure" now becomes a use case, and so we're finally in a position to exploit the power of procedural AND object-oriented design and programming! (and yes, I am totally serious)<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">So in the end, I think that most applications have a place for WF, because most applications have one or more of these non-interactive processes. The design effort is worth it, because the end result is a more flexible and maintainable process within your application.</font></font></font>
