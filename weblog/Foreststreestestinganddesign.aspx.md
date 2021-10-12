---
title: Forests, trees, testing and design
postDate: 2006-03-31T11:05:09.984-05:00
abstract: Oops, I guess I upset the TDD people :)
postStatus: publish
---
31 March 2006

<font face="Times New Roman" color="#000000" size="3">During the early banter-and-have fun part of my recent dotnetrocks interview I dissed TDD (Test Driven Development, not the text translation service for the deaf). Of course this wasn’t the focus of the real interview, and prior to sitting down behind the mic I hadn’t thought about TDD at all, so we were all just having some fun. As such, it was flippant and it was short - meaning I was having fun, and that I surely didn't have the time or opportunity to really express my thoughts on design or testing. That would be an entirely different show all by itself.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>
<font face="Times New Roman" color="#000000" size="3"><p class="MsoNormal" style="MARGIN: 0in 0in 0pt">Nor do I have time to write a long discussion of my thoughts on design, or on testing, just at the moment. But I did respond to some of the comments on <a href="http://www.ayende.com/Blog/ct.ashx?id=63e46857-3d82-4332-b5cd-99b4b64f2a88&amp;url=http%3a%2f%2fcodebetter.com%2fblogs%2fjeffrey.palermo%2farchive%2f2006%2f03%2f28%2f141920.aspx">Jeffery Palermo’s blog</a> – and here are some more thoughts:</p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt"></p></font><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>
<font face="Times New Roman" color="#000000" size="3">As a testing methodology TDD (as I understand it) is totally inadequate. I was unable to express this point in the interview due to the format, but the idea that you’d have developers write your QA unit tests is unrealistic. And it was pointed out on <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:place w:st="on"><st1:city w:st="on">Palermo</st1:city></st1:place>’s blog that TDD isn’t about writing comprehensive tests anyway, but rather is about writing a <i style="mso-bidi-font-style: normal">single</i> test for the method – which is exceedingly limited from a testing perspective. </font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Of course you could argue that since the <i style="mso-bidi-font-style: normal">vast</i> majority of applications have no tests <i style="mso-bidi-font-style: normal">at all</i>, that it is a huge win if TDD can get companies to write just one test per method. That is infinitely better than the status quo (that whole division by zero thing) and so TDD is hugely beneficial regardless of whether it is actually the best approach or not. I’d go with this: <i style="mso-bidi-font-style: normal">some</i> testing is better than <i style="mso-bidi-font-style: normal">no</i> testing. But one-test-per-method is pretty lame and certainly doesn’t qualify as <i style="mso-bidi-font-style: normal">real</i> testing.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">But the real key is that developers are <i style="mso-bidi-font-style: normal">terrible</i> testers (with perhaps a few exceptions). This is because developers test to make sure something works. Actual testers, on the other hand, test to find ways something <i style="mso-bidi-font-style: normal">doesn't</i> work. Testers focus on the edge cases, the exceptional cases, the scenarios that a developer (typically?) ignores. Certainly there's no way to provide this level of comprehensive test in a <em>single</em> test against a method - which really supports another person's comment on Palermo's blog: that TDD isn't about testing.</font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Having spent a few months being employed specifically to do that type of QA unit testing I can tell you that I suck at it. I just don't think in that "negative" manner, and it is serious effort for me to methodically and analytically work my way through every possible permutation in which a method can be used and misused. I’ve observed that this is true for virtually all developers. As a group, we tend to be optimists – testing only to make sure things work, not to find out if they fail. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">But as someone on <st1:city w:st="on"><st1:place w:st="on">Palermo</st1:place></st1:city>'s blog pointed out, TDD is mis-named. TDD isn't about testing (thankfully), nor apparently is it about development. It is, he said, a design methodology.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">That's fine, but I don't buy into TDD as a “design methodology" either. You can't "design" a system when you are focused at the method level. There’s that whole forest-and-trees thing... Of course </font><font face="Times New Roman" color="#000000" size="3">I am not a TDD expert – by a long shot – so for all I know there’s some complimentary part of TDD that looks at the forest level. </font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">But frankly I don’t care a whole lot, because I use a modified CRC (class, responsibility and collaboration) approach. This approach is highly regarded within the agile/XP community, and is to my mind the best way to do OOD that anyone has come up with to this point. (David West's <a href="http://www.microsoft.com/mspress/books/6820.asp">Object Thinking</a> book really illustrates how CRC works in an agile setting)&nbsp;</font><font size="3"><font color="#000000"><font face="Times New Roman">The CRC approach I use sees the forest, then carefully focuses in on the trees, pruning back the brush as needed.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Now I could see where TDD (as I understand it) would be complimentary to CRC, in that it could be used to write the prove-it-works tests for the objects' methods&nbsp;based on the OO model from CRC – but I’m speculating that this isn’t what the TDD people are after. Nor do I see much value at that point – because the design is done, so whether you write the test before or immediately after doesn't really matter - the test isn't driving the design.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But to my mind writing the tests is a <i style="mso-bidi-font-style: normal">must</i>. In the interview I mentioned that I (like all developers) have always written little test harnesses for my code. What I didn’t get to say (due to the banter format) was that for years now I’ve been writing those tests in nunit, so they provide a form of continual regression testing. In talking to </font>[<font face="Times New Roman" size="3">Jim Newkirk</font>](http://blogs.msdn.com/jamesnewkirk/)<font face="Times New Roman" color="#000000" size="3"> about TDD and his views on this, he said that this is exactly what he does and recommends doing.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And as long as we all realize that these are <i style="mso-bidi-font-style: normal">developer</i> tests, and that some real <i style="mso-bidi-font-style: normal">quality assurance</i> tests are also required (and which should be written by test-minded people) then that is good. Certainly this is my view: developers <i style="mso-bidi-font-style: normal">must</i> write nunit tests (or use VSTS or whatever), and that I <i style="mso-bidi-font-style: normal">strongly</i> encourage clients to hire real testers to complete the job – to flesh out the testing to cover edge and exceptional cases.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">None of which, of course, is part of the design process, because that’s done using a modified CRC approach.</font>
