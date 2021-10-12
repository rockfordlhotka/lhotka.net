---
title: Strongly typed DataPortal_XYZ methods in CSLA .NET 2.0
postDate: 2005-11-18T18:02:25.531-06:00
abstract: Thanks to prodding by Jason Bock, this is a major improvement to the DataPortal
postStatus: publish
---
18 November 2005

<font face="Times New Roman" color="#000000" size="3">I’ve posted a couple times before about what a business class will look like in the next edition of my </font>[<font face="Times New Roman" size="3">business objects books</font>](http://www.lhotka.net/cslanet)<font face="Times New Roman" color="#000000" size="3"> and thus in CSLA .NET 2.0. One of those times </font>[<font face="Times New Roman" size="3">Jason Bock</font>](http://www.jasonbock.net/JB/Default.aspx)<font face="Times New Roman" color="#000000" size="3"> (a fellow </font>[<font face="Times New Roman" size="3">Magenicon</font>](http://www.magenic.com/)<font color="#000000"><font face="Times New Roman" size="3">) sent me an email asking why the </font><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">DataPortal_Create/Fetch/Delete</span><font face="Times New Roman" size="3"> methods aren’t strongly typed. </font></font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If you look at the current approach and what I’ve posted thus far for the next edition you’ll see code like this:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">Protected Overrides Sub DataPortal_Fetch(ByVal criteria As Object)<o:p></o:p></font>

<font face="Times New Roman" color="#000000" size="3">or</font>

<font color="#000000">protected override void DataPortal_Fetch(object criteria)<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Jason’s comment got me thinking. The DataPortal uses reflection to invoke this method, so why not be a bit more thorough in identifying the method’s parameters and invoke a strongly typed version like this:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">Private Overloads Sub DataPortal_Fetch(ByVal criteria As Criteria)<o:p></o:p></font>

<font face="Times New Roman" color="#000000" size="3">or</font>

<font color="#000000">void DataPortal_Fetch(Criteria criteria)<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><font face="Times New Roman" size="3">Where </font><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">Criteria</span><font face="Times New Roman" size="3"> is the actual type of the criteria object provided when calling the </font><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">DataPortal.Fetch()</span><font face="Times New Roman" size="3"> method back in the factory.</font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><font face="Times New Roman" size="3">(the </font><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">Overloads</span><font face="Times New Roman" size="3"> keyword is required because the base class still implements the default protected version)</font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><font face="Times New Roman" size="3">As with many things, this sounded relatively trivial but turned out to be somewhat harder than expected. It is always the edge cases that make things hard… In this case the hard part is that parameters could be </font><span class="NormalCourierNewChar"><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">Nothing</span></span><font face="Times New Roman" size="3"> – in which case you don’t know what type they would be if they weren’t </font><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">Nothing</span><font face="Times New Roman" size="3">...</font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">After working through that issue all is well.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This (in my opinion) is better than the alternative, which was to go with an interface-based approach and formalize the late-bound concept. That has its attraction, and people have altered CSLA .NET 1.0 along that line, but I really prefer strong typing if I can get it.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><font face="Times New Roman" size="3">In particular this is nice for collections, where you may have multiple criteria classes for different views – now you can just implement a strongly-typed </font><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">DataPortal_Fetch()</span><font face="Times New Roman" size="3"> method for each criteria class. Very clean and nice.</font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><font face="Times New Roman" size="3">I’m still deliberating over whether to leave the default protected implementations in the base classes. They are nice because VS helps you override those methods, but they aren’t optimal. Given that VS has such nice snippet support it may be better to drop the protected defaults and just rely on snippets to insert the </font><span style="FONT-SIZE: 10pt; FONT-FAMILY: 'Courier New'">DataPortal_XYZ</span><font face="Times New Roman" size="3"> methods.</font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If you have an opinion, feel free to comment :)</font>
