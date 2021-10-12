---
title: Web services, DataSets and now...Business Objects
postDate: 2005-01-24T10:10:21.296-06:00
abstract: Sahil has some interesting thoughts on the web service/DataSet question as well, but I disagree with his portrayal of business objects.
postStatus: publish
---
24 January 2005

<font face="Times New Roman" color="#000000" size="3">Sahil has some <a href="http://dotnetjunkies.com/WebLog/sahilmalik/archive/2005/01/23/47832.aspx">interesting thoughts</a> on the web service/DataSet question as well.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">He spends some time discussing whether “business objects” should be sent via a web service. His definition of “business object” doesn’t match mine, and is closer to Fowler’s data transfer object (DTO) I think.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is important to remember that web services <i style="mso-bidi-font-style: normal">only</i> move boring data. No semantic meaning is included. At best (assuming avoidance of xsd:any) you get some limited syntactic meaning along with the data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">When we talk about moving <i style="mso-bidi-font-style: normal">anything</i> via a web service, we’re really just talking about data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">When talking about moving a “business object”, most people think of something that can be serialized by web services – meaning by the XmlSerializer. Due to the limitations of the XmlSerializer this means that the objects will have all their fields exposed as public fields or read-write properties.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">What this means in short, is that the “business objects” can <i style="mso-bidi-font-style: normal">not</i> follow good OO design principles. Basically, they are not “business objects”, but rather they are a way of defining the message schema for the web service. They are, at best, data transfer objects.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In my business objects books and framework I talk about moving actual business objects across the wire using remoting. Of course the reality here is that only the data moves – but the code must exist on both ends. The effective result is that the object is cloned across the network, and retains both its data and the semantic meaning (the business logic in the object).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">You can do this with web services too, but not in a “web service friendly” way. Cloning an object implies that you get <i style="mso-bidi-font-style: normal">all</i> the data in the object. And to do this while still allowing for encapsulation means that the serialization must get private, friend/internal and protected fields as well as public ones. This is accomplished via the BinaryFormatter. The BinaryFormatter generates and consumes streams, which can be thought of as byte arrays. Thus, you end up creating a web service that moves byte arrays around. Totally practical, but the data is not human-readable XML – it is Base64 encoded binary data. I discuss </font>[<font face="Times New Roman" size="3">how to do this in CSLA .NET</font>](/Articles.aspx?id=1f6614eb-cf8b-4b30-abc2-b2558cb23348)<font face="Times New Roman" color="#000000" size="3"> on my web site.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman"><i style="mso-bidi-font-style: normal">Now</i> we are talking about moving business objects. Real live, OO designed business objects.</font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course this approach is purely for n-tier scenarios. It is totally antithetical to any service-oriented model! </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">For an SO model you need to have clearly defined schemas for your web service messages, and those should be independent from your internal implementation (business objects, DataSets or whatever). I discuss this in Chapter 10 of my </font>[<font face="Times New Roman" size="3">business objects books</font>](/cslanet)<font face="Times New Roman" color="#000000" size="3">.</font>


