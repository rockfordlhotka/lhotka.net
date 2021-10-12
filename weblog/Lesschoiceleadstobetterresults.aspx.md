---
title: Less choice leads to better results?
postDate: 2005-01-07T22:23:13.640625-06:00
abstract: If less choices lead to better results, then higher level languages and frameworks truly are the way of the future.
postStatus: publish
---
07 January 2005

1. <font face="Times New Roman" color="#000000" size="3">Less choice leads to better results.</font>
2. <font face="Times New Roman" color="#000000" size="3">Higher level languages and frameworks restrict choice.</font>
3. <font face="Times New Roman" color="#000000" size="3">Thus, higher level languages and frameworks should lead to better results.</font>


<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The &#8220;less choice&#8221; statement flows from this article entitled </font>[<font face="Times New Roman" size="3">Choice Cuts</font>](http://www.tnr.com/doc.mhtml?pt=RWWYoJx8t4LLEwVD7Mx30h==&amp;zx=1a70c06a9c023bb236246010)<font face="Times New Roman" color="#000000" size="3">. Ignore the politics and focus on the research beneath the statement. That&#8217;s what is valuable in this context.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is obvious that higher level languages and frameworks restrict choice, so I&#8217;m not going to cite a bunch of references for that. While many of these languages and frameworks provide a way to drop out to a lower level, in and of themselves they restrict choice. Just look at Visual Basic versions 1-6. Very productive, but often restrictive.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Whether the conclusion that higher level languages and frameworks will lead to better results is true or not is unknown. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Certainly there are examples where better results have been gained. This train of thought is lurking somewhere behind the software factories movement, and does seem quite compelling. Certainly many people using </font>[<font face="Times New Roman" size="3">CSLA .NET</font>](/cslanet)<font face="Times New Roman" color="#000000" size="3"> with code generators have found radically increased productivity &#8211; and the combination of the two does restrict choice.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Yet there are countless examples (especially from the era of CASE tools) where the results were totally counter-productive. Where restriction of choice forced intricate workarounds that <i style="mso-bidi-font-style: normal">decreased</i> productivity and made things worse.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Charles Simonyi </font>[<font face="Times New Roman" size="3">contributed to an article</font>](http://www.edge.org/q2005/q05_3.html)<font face="Times New Roman" color="#000000" size="3"> on The Edge, essentially noting that there still is a software crisis and that low-level languages aren&#8217;t solving the problem. He argues in fact, that low-level languages like C#, VB and Java are a dead-end. That we must move to higher-level language concepts in order to adequately represent the real world through software.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This is the view of the software factories people and the domain-specific language movement. And it is rather hard to argue the point. There are many days when I feel like I&#8217;m writing the same code I wrote 15 years ago &#8211; except now its in a GUI instead of on a VT100 terminal. But the business code just hasn&#8217;t changed all that terribly much&#8230;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To look at it a different way, a software architect&#8217;s job is to restrict choice. Our job in this role is to look at the wide array of choices and narrow them down to a specific set that our organization can use. Why? Because having each developer or project lead do all that filtering would seriously cut into productivity.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Companies employ architects specifically to limit choice. To set standards and policies that narrow the technology focus to a limited set of options. The rest of the organization then lives within those artificial boundaries. There are many reasons for this, including licensing costs, training and so forth. I doubt that many people have considered the direct (presumably positive) impact of the reduction of choice however.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I&#8217;ve been working on an idea I&#8217;ve dubbed an Entity Description Language (EDL). My original motivation was to reduce the amount of plumbing code we write. Look at a typical Java, C# or VB class and you&#8217;ll find that less than 4% of the actual lines in the class perform tangible business functions. Most of the lines are just language syntax or pure plumbing activities like opening a database connection.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In working on EDL though, I&#8217;ve discovered that it is virtually impossible &#8211; and perhaps undesirable &#8211; to replicate the capabilities of C# or VB in their entirety. There are <i style="mso-bidi-font-style: normal">reasons</i> why these languages use such a verbose syntax. They require verbosity in order to provide flexibility, or choice. Virtually unlimited choice.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If we now consider that <i style="mso-bidi-font-style: normal">limited</i> choice is better, then perhaps the fact that something like EDL restricts choice is only good&#8230;</font>
