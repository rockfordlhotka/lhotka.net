---
title: Long live procedural programming (or was that service-oriented programming?)
postDate: 2004-09-03T09:04:15.734375-05:00
abstract: In some previous posts on service-oriented architecture (SOA), I got comments from various people indicating that SO could/should be applied inside applications as well as between applications. I am skeptical about this - here's why.
postStatus: publish
---
03 September 2004

In some previous posts on service-oriented architecture (SOA), I got comments from various people indicating that SO could/should be applied *inside* applications as well as between applications. I am skeptical about this - here's why.

Attempting to apply service-oriented concepts *inside* an application is non-trivial. This is exactly what we tried to do in FORTRAN, C and other languages years ago.

At the time we all argued that it was a good idea - procedural programming made a lot of sense. If you passed all required data in via paramters, and got all data out as a result then procedures were a great way to encapsulate behavior. In this context a procedure of yesteryear and a service of tomorrow are really the same thing.

Of course it didn't actually work that way. Packaging all the data into the parameters was often a huge task, and so virtually everyone cheated by using a common block of memory or other global variable techniques. Thus procedural programming was brought to its knees, because procedures didn't “own” the data on which they operated.

This is a core flaw in object-oriented (OO) designs as well. It is very common to pass an object as a parameter and have some method act on the object. But what you really pass is an object *reference*. The actual object is conceptually similar to a common block in that case.

Now I agree that OO avoids many flaws of procedural programming, but the fact that methods end up acting on the same physical set of data (objects) can be problematic.

So to apply SO (service-oriented) concepts *inside* an application means that we're going to take the procedural approach from FORTRAN, but this time we're not going to cheat. Instead we're going to package all the required data into a message (not an object, because the message must be passed by value!!!) and pass it to the procedure (service).

As with FORTRAN years ago, I agree that this *could* be done. But we didn't have the discipline then, and I very much doubt we have the discipline now. It is just too damn much work to create an XML document (or whatever) each time I need to call a method, and then to unpack an XML document to get at the result. It is simply unrealistic to expect that developers are going to go through this much work.

And people today complain about code bloat. Think of the bloat we're talking about here. Rather than putting an integer on the stack to call a method, we're now going to put the integer into XML and put the XML on the stack? Good thing Moore's Law is out there to save our collective asses...

This is not to say that SO won't work *between* applications. In that case it will (I think) work very nicely, because you can't cheat. It isn't possible to use a common block or reference to an object across process or network boundaries, so we have to pack parameters and pass them by value.

In the end, SO is what FORTRAN and C were meant to be - and without the possibility of cheating it might really work. Long live procedural programming!
