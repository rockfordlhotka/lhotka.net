---
title: DataSets – not all they could be
postDate: 2005-08-29T10:37:15.53125-05:00
abstract: Thinking out loud
postStatus: publish
---
29 August 2005

<font face="Times New Roman" color="#000000" size="3">I just got back from a week’s vacation/holiday in <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:country-region w:st="on"><st1:place w:st="on">Great Britain</st1:place></st1:country-region> and I feel very refreshed.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And that’s good, given that just before going to the <st1:country-region w:st="on"><st1:place w:st="on">UK</st1:place></st1:country-region> I wrapped up the first draft of Chapter 1 in the new book Billy Hollis and I are writing. As you have probably gathered by now, this book uses DataSet objects rather than my preferred use of business objects.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I wanted to write a book using the DataSet because I put a lot of time and energy into lobbying Microsoft to make certain enhancements to the way the objects work and how Visual Studio works with them. Specifically I wanted a way to use DataSet objects as a </font>[<font face="Times New Roman" size="3">business layer</font>](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=efa88d0a-2388-4909-bee1-c9bddb6e9868)<font face="Times New Roman" color="#000000" size="3"> – both in 2-tier and n-tier scenarios.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Also, I wanted to write a book using Windows Forms rather than the web. This reflects my bias of course, but also reflects the reality that intelligent/smart client development is making a <i style="mso-bidi-font-style: normal">serious</i> comeback as businesses realize that deployment is no longer the issue it was with COM and that development of a business application in Windows Forms is a <i style="mso-bidi-font-style: normal">lot</i> less expensive than with the web.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The book is geared toward professional developers, so we assume the reader has a clue. The expectation is that if you are a professional business developer (</font>[<font face="Times New Roman" size="3">a Mort</font>](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=9a45f49b-6790-4243-a747-419b064497d4)<font face="Times New Roman" color="#000000" size="3">) that uses VB6, Java, VB.NET, C# or whatever – that you’ll be able to jump in and be productive without us explaining the trivial stuff.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So Chapter 1 jumps in and creates the sample app to be used throughout the book. The chapter leverages all the features Microsoft has built into the new DataSet and its Windows Forms integration – thus showing the good, the bad and the ugly all at once.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Using partial classes you really can embed most of your validation and other logic into the DataTable objects. When data is changed at a column or row level you can act on that changed data. As you validate the data you can provide text indicating why a value is invalid.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The bad part at the moment is that there are bugs that prevent your error text from properly flowing back to the UI (through the ErrorProvider control or DataGridView) in all cases. In talking to the product team I believe that my issues with the ErrorProvider will be resolved, but that some of my DataGridView issues won’t be fixed (the problems may be a “feature” rather than a bug…). Fortunately I was able to figure out a (somewhat ugly) workaround to make the DataGridView actually work like it should.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The end result is that Chapter 1 shows how you can create a DataSet from a database, then write your business logic in each DataTable. Then you can create a basic Windows Forms UI with virtually no code. It is really impressive!!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But then there’s another issue. Each DataTable comes with a strongly-typed TableAdapter. The TableAdapter is a very nice object that handles all the I/O for the DataTable – understanding how to get the data, fill the DataTable and then update the DataTable into the database. Better still, it includes atomic methods to insert, update and delete rows of data directly – without the need for a DataTable at all. Very cool!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Unfortunately there are no hooks in the TableAdapter by which you can apply business logic when the Insert/Update/Delete methods are called. The end result is that any validation or other business logic is pushed into the UI. That’s terrible!! And yet that’s the way my Chapter 1 works at the moment…</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This functionality obviously isn’t going to change in .NET or Visual Studio at this stage of the game, meaning that the TableAdapter is pretty useless as-is.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">(to make it worse, the TableAdapter code is in the same physical file as the DataTable code, which makes n-tier implementations seriously hard)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Being a framework kind of guy, my answer to these issues is a framework. Basically, the DataTable is OK, but the TableAdapter needs to be hidden behind a more workable layer of code. What I’m working through at the moment is how much of that code is a framework and how much is created via code-generation (or by hand – ugh).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But what’s really frustrating is that Microsoft could have solved the entire issue by simply declaring and raising three events from their TableAdapter code so it was possible to apply business logic during the insert/update/delete operations… Grumble…</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">The major bright point out of all this is that I know business objects solve all these issues in a superior manner. Digging into the DataSet world merely broadens my understanding of how business objects make life better.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Though to be fair, the flip side is that creating simple forms to edit basic data in a grid is almost infinitely easier with a DataTable than with an object. Microsoft really nailed the trivial case with the new features - and that has its own value. While frustrating when trying to build <em>interesting</em> forms, the DataTable functionality does mean you can whip out the boring maintenance screens with just a few minutes work each.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Objects on the other hand, make it comparatively easy to build interesting forms, but require more work than I'd like for building the boring maintenance screens...</font>
