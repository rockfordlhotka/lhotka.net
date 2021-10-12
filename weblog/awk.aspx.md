---
title: awk
postDate: 2005-02-21T09:29:49.953125-06:00
abstract: I wonder why there isn't either a variant of XSLT that can do what awk does, or a variant of awk that parses XML documents like XSLT. Perhaps the world just isn't ready for that kind of power?
postStatus: publish
---
21 February 2005

A few days ago I [posted a list of programming languages](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=6a2b69a1-2095-4f59-a4f7-c2892e445280) in which I've been competent over the years. A few other people chimed in with their own lists, which I found very interesting.



[Thomas Williams](http://dotnetjunkies.com/WebLog/thomasswilliams/archive/2005/02/16/54513.aspx) pointed out that XSLT was important in his history, which got me thinking about an oversight in my own list.



I neglected to mention awk (more specifically gawk on the VAX). awk is a unix text processing language, and [gawk](http://www.gnu.org/software/gawk/gawk.html) is the GNU Project version created for many platforms. I first learned about awk when taking a graduate level data structures class at the University of Minnesota where we used Unix boxes of some flavor or other. It was so useful that I found the VAX gawk implementation and put that on our VAX at work (this was around 1990 or so).



People rave about things like perl or XSLT, but I gotta say that for pure text processing it is hard to be awk. If XSLT had the power of awk it would have swept the web development world in ways we can't even imagine. I know that XSLT is widely used in the web world, but if you've used XSLT and haven't used awk you just don't know how crippled XSLT really is.



The thing is, that XSLT has the same mindset as awk. An awk program is divided up into blocks, and each block is triggered based on a regular expression evaluation. In the case of awk, each input line is evaluated against the regular expression for every block. Each block where the regular expression matches the input line is executed. There is no linear or event-driven or OO concept involved. It is the same as XSLT in this regard.



Where awk is amazing is that it is a complete language. It has variables, arrays, looping structures, conditionals and so forth. The input text is automatically parsed into easy-to-manipulate chunks based on your parsing choices. This means that inside one of these blocks, you can do virtually anything you desire. So within a block, triggered due to a regular expression match, you can use a complete programming language that is entirely geared toward text manipulation to act on a pre-parsed line of input.



To this day I wonder why there isn't either a variant of XSLT that can do what awk does, or a variant of awk that parses XML documents like XSLT. Perhaps the world just isn't ready for that kind of power?
