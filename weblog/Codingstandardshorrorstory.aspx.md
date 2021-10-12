---
title: Coding standards horror story
postDate: 2016-12-22T12:30:01-06:00
abstract: 
postStatus: publish
---
22 December 2016

Early in my career, actually my first "real" job, I worked for a guy named Mark. Mark was an amazingly smart and driven programmer and I learned a lot from him.

But he and I would butt heads constantly over coding standards and coding style.

Our platform was the DEC VAX and our code was written using VAX Basic. For this story to make sense, you must realize that VAX Basic wasn't really BASIC the way you typically think about it. The DEC compiler team had started with Basic syntax and then merged in all the goodness of FORTRAN and Modula II and Pascal. For example, even back in the late 1980's the language had structured error/exception handling.

It is also important to understand that in the late 1980's there weren't code editors like Visual Studio. We used something called TPU (Text Processing Utility) that was more powerful than Notepad by far, but nothing compared to modern editors of today. It competed with Emacs and vi. As a result, it was up to the *developer* to style their code, not the editing tool.

Mark had defined a strict set of coding standards and a style guide, and he'd dial back into work from home at night to review our code (yes, via at 1200 baud modem at the time). It was not uncommon to come into work the next day and have a meeting in Mark's office where he'd go through the styling mistakes in my code so I could go fix them.

He defined things like every line would start with a tab, then 2 spaces. Or two tabs, then 2 spaces. Why the 2 spaces? I still have no idea, but that was the standard. He had a list of language keywords that were off limits. Roughly half the keywords were forbidden in fact. He defined where the `Then` would go after an `If`; on the next line down, indented.

I chafed at all of this. The 2 space thing was particularly stupid in my view, as was making all those fun keywords off limits. I can't say I cared about the `Then` statement one way or the other, except that it forced me to type *yet another line* with the stupid 2 space indent.

But what are you going to do? Mark was the boss, and this was my first job out of university in the late 1980's Reagan-era recession. In a job environment where thousands of experienced computer programmers were being laid off in Minnesota I wasn't going to risk my job.


> Which isn't to say that I didn't argue - anyone who knows me knows that I can't keep my opinions to myself :)


The thing is, after a period of time it seems like *any* standard becomes second nature. I just internalized Mark's rules and coded happily away. In fact, what I found is that my "artistic expression" wasn't really crippled by the guidelines, I just had to learn how to be artistic within them.

Knowing a few artists, I'm now aware that putting boundaries around what you do is *key* to creating art. Artists pretty much always limit themselves (often artificially) so they have a context in which to work. Not that I think code is 100% art, but I do think that there's art in good code.

Several months after starting to work with Mark, and absorbing this rigorous standards-based approach to coding, our company was purchased by another company. Mark, myself, and a couple other employees survived this process. And we all moved from Minnesota to Birmingham, AL; which is another story entirely. Let me just say here that regional culture differences *within* the US are easily comparable to the difference between the US and many European countries.

The company that bought my employer was also a software company, with a dev team of comparable size to what we'd had. But they had *no coding standard* or guideline. They did use the DEC VAX, and they did use VAX Basic. But each developer did whatever they wanted without regard for anyone else.

One of the developers cut his teeth on FORTRAN. It turns out that VAX Basic could be made to look *exactly* like FORTRAN. Remember that DEC merged most of the good features of FORTRAN into VAX Basic after all.

Another developer clearly learned to program on an Apple ][ and his VAX Basic code had *line numbers*. I kid you not!! Just like Applesoft!

My point is that everyone in that dev shop had *radically* different coding styles and approaches. Some very ancient and creaky (even by 1989 standards), and some quite modern. It turns out they'd done this all intentionally. Partly because none of them wanted to learn anything particularly new. And mostly because it provided a sort of job security, because it was essentially impossible for any of them to maintain anyone else's code.

Contrast this to Mark's world, where it was impossible to tell who'd written any bit of code, because all code used the same style and structure.

This was the point where I had my first professional developer epiphany. Yes, it is truly painful to adapt to the idea of living within strict coding and style guidelines. But the alternative is *so much worse*!

Ever since that experience I insist on consistency of coding standards and styles within each project (or enterprise) where I work. And even if I think some choices (like 2 spaces after each tab) are really, really, really stupid, I'll use and vehemently support that choice.


> Which, again, isn't to say that I won't argue a little up front about anything that seems really dumb, but once the decision is made, it is made.


I learned a lot from Mark. Some good, some bad. But this particular lesson is one that is central to my view of good software development.
