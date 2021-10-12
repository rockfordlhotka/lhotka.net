---
title: SOA, dollar signs and trust boundaries
postDate: 2004-04-08T10:27:35.203125-05:00
abstract: Rocky shares some of his thoughts on Service-Oriented Architecture (SOA), including how it will make a lot of money for vendors, and some ways customers can think about and apply SOA to minimize that profit-taking.
postStatus: publish
---
08 April 2004

<font face="Times New Roman" color="#000000" size="3">A number of people have asked me about my thoughts on SOA (service-oriented architecture). I have a great deal of interest in SOA, and a number of fairly serious thoughts and concerns about it. But my first response is always this.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The S in SOA is actually a dollar sign ($OA).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is a dollar sign because SOA is going to cost a lot of people a lot of money, and it will make a lot of other people a lot of money.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It will make money for product vendors, as they slap the SOA moniker on all sorts of tools and products around web service creation, consumption and management. And around things like XML translators and transformers, and queue bridging software and transaction monitors and so forth. Nothing particularly new, but with the SOA label, these relatively old concepts become fresh and worthy of high price tags.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It will make money for service vendors (consultants) in a couple ways. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The first are the consultants that convince clients that SOA is the way to go &#8211; and that it is big and scary and that the only way to make it work is to pay lots of consulting dollars. SOA, in this world-view, involves business process reengineering, rip-and-replace of applications, massive amounts of new infrastructure (planning and implementation) and so forth.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The second are the consultants who come in to clean up after the first group make a mess of everything. This second group will also get to clean even after many clients who didn&#8217;t spend on big consulting dollars, but bought into the product vendors&#8217; hype around SOA and their quasi-related products.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Who loses money? The clients who buy the hyped products, or fall for the huge consulting price tags due to FUD or the overall hype of SOA.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Since I work in consulting, SOA means dollars flowing toward me, so you&#8217;d think I&#8217;d be thrilled. But I am not. This is a big train wreck just waiting to derail what should be a powerful and awesome architectural concept (namely SOA).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So, in a (most likely vain) effort to head this off, here are some key thoughts.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

1. <font face="Times New Roman" color="#000000" size="3">SOA is not about products, or even about web services. It is an architectural philosophy and concept that should drive enterprise and application architecture.<br style="mso-special-character: line-break"><br style="mso-special-character: line-break"></font>
2. <font face="Times New Roman" color="#000000" size="3">SOA is not useful INSIDE applications. It is only useful BETWEEN applications. <br><br>If you think you can replace your TIERS with SOA concepts, you are already in deep trouble. Unless you turn your tiers into full-blown applications, you have no business applying SOA between them.<br style="mso-special-character: line-break"><br style="mso-special-character: line-break"></font>
3. <font face="Times New Roman" color="#000000" size="3">Another way to look at #2 is to discuss trust boundaries. Tiers within an application trust each other. That&#8217;s why they are tiers. Applications don&#8217;t trust each other. They can&#8217;t, since there&#8217;s no way to know if different applications implement the same rules the same ways.<br><br>SOA is an idea philosophy and concept to help cross trust boundaries. If you don&#8217;t cross a trust boundary, you don&#8217;t want SOA in there causing complexity. But if you do cross a trust boundary, you want SOA in there helping you to safely manage those trust and connectivity issues.<br style="mso-special-character: line-break"><br style="mso-special-character: line-break"></font>
4. <font face="Times New Roman" color="#000000" size="3">To turn #3 around, if you are using SOA concepts, then you are crossing a trust boundary. Even if you didn&#8217;t plan for, or intend to insert a trust boundary at that location in your design, you just did.<br><br>The side-effect of this is that anywhere that you use SOA concepts between bits of code, those bits of code must become applications, and must stop trusting each other. Each bit of code must implement its own set of business rules, processing, etc. <br><br>Thus, sticking SOA between the UI and middle tiers of an application, means that you now have two applications &#8211; one that interacts with the user, and one that interacts with other applications (including, but obviously not limited to your UI application). Because you&#8217;ve now inserted a trust boundary, the UI app can&#8217;t trust the service app, nor can the service app trust the UI app. Both apps must implement all your validation, calculation, data manipulation and authorization code, because you can&#8217;t trust that either one has it right. <br><br>More importantly, you can&#8217;t trust that FUTURE applications (UI or service) will have it right, and SOA will allow those other application to tap into your current applications essentially without warning. This, fundamentally, is why inserting SOA concepts means you have inserted a trust boundary. If not today, in the future you WILL have untrusted applications interacting with your current applications and they&#8217;ll try to do things wrong. If you aren&#8217;t defensive from the very start, you&#8217;ll be in for a world of hurt.</font>


<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In the end, I think the trust boundary mindset is most valuable guide for SOA. Using SOA is expensive (in terms of complexity and performance). It is not a price you should be willing to pay to have your UI talk to a middle tier. There are far simpler, cheaper and faster philosophies, concepts and technologies available for such interaction.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">On the other hand, crossing trust boundaries is expensive and complex all by itself. This is because we have different applications interacting with each other. It will always be expensive. In this case, SOA offers a very nice way to look at this type of inter-application communication across trust boundaries, and can actually decrease the overall cost and complexity of the effort.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>


