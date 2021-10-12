---
title: On the use and misuse of patterns
postDate: 2010-07-19T12:03:04.0536896-05:00
abstract: 
postStatus: publish
---
19 July 2010

I was just at a family reunion and heard a joke about the comedian’s retirement home. A guy walks into the common room and hears one old guy shout out “19”, and everyone laughs. Across the room another guy shouts out “54” and everyone laughs even harder. The guy turns to his guide and asks “What is going on?”. The guide replies “These guys know all the same jokes, and at their age it takes too long to tell them, so they just assigned them all numbers.” The guy smiles, and shouts out “92”, which results in a just a few grudging chuckles. “What’d I do wrong?” he asks the guide. The guide replies “Some people can tell a joke, some people can’t.”

That made me think about patterns (yes, I know, I’m a geek).

I like design patterns. Who wouldn’t? They are a formalized description of a solution to a specific problem. If you have that problem, then having a formally described solution seems like a dream come true.

Perhaps more importantly patterns are a language short-cut. If everyone in a conversation understands a pattern, the pattern (and often its problem) can be discussed merely by using the pattern name, which saves an immense amount of time as opposed to describing the actual problem and solution in detail.

Of course the “formalized description” is prose. Human language. And therefore it is ambiguous and open to interpretation. The descriptions *must be human-readable*, because any pattern worth ink and paper transcends any specific platform or programming language. Describing a “pattern” in Java or C# is silly – because that makes it far too likely that it isn’t really a broad pattern, but is simply a practice that happens to work in a given language or on a given platform.

But this ambiguity leads to trouble. Not unlike the comedian’s retirement home, patterns are a short-cut language to some really complex concepts, and often even more complex implementations. While everyone *might* have a basic comprehension of “inversion of control”, I can guarantee you that saying IoC doesn’t bring the same concept, implementation or emotional response from everyone who hears it.

Pattern zealots often forget (or overlook) the fact that patterns have consequences. Good and bad consequences. *Every pattern has bad consequences*, as well as good ones. Some people get attached to a pattern because it helped them at some point, and they just assume that pattern will *always* have a positive or beneficial result. But that’s simply not true. Sometimes the negative consequences of a pattern outweigh the positive – it is all very dependent on the specific problem domain and environment.

Soft things like staffing levels, skill sets, attitudes and time frames all enter into the real world environment. Add the reality that any given problem almost certainly has *several patterns* that provide solutions – for different variations of the problem – and it becomes clear that no one pattern is always “good”.

It should come as no surprise then, that patterns are often misused – in several different ways.

My pet peeve is when a pattern is applied because something likes the pattern, not because the application actually has the problem the pattern would solve. I often see people using IoC, for example, because it is trendy, not because they actually need the flexibility provided by the pattern. They use a container to create instances of objects *that they will never swap out for other implementations*. What a waste – they’ve accepted all the negative consequences of the pattern *for absolutely no benefit* since they don’t have the problem the pattern would solve. Is this the fault of IoC? Of course not, IoC is a powerful pattern.

It is the fault of what I call the “Pattern Of The Year” (POTY) syndrome. When a pattern becomes really popular and trendy, it becomes the POTY. And everyone wants to go to the POTY. If you need the POTY, you should go. But if you don’t need the POTY, it is really a little silly (if not creepy) for you to go to the POTY…

**In short: only use a pattern if you have the problem it solves, and the positive consequences outweigh the negative consequences.**

Perhaps the most common misuse of patterns is failure to actually understand the pattern or its implementation. To stick with IoC as an example, it is pretty common for a development team to completely misunderstand the pattern or the framework that implements the pattern. Sure, some architect or lead developer “got it” (or so we hope) which is why the team is using the pattern – but you can find apps where numerous competing containers are created, each initialized differently.

I always thought Apple BASIC spaghetti code was the worst thing possible – but misuse of certain design patterns quickly creates a mess that is an order of magnitude worse than anything people wrote back in the early 80’s…

**In short: if you use a pattern, make sure your *entire team* understand the pattern *and your implementation of the pattern*.**

As I mentioned earlier, most problems can be solved by more than one pattern. Any truly interesting problem almost certainly has multiple solutions, each with different good/bad consequences and various subtle differences in outcome. It is not uncommon for the best solution to be a combination of a few more basic patterns.

As an example, the CSLA data portal is a combination of around six basic design patterns that work together in concert to solve the problem space the data portal targets. I’m not saying the data portal is a design pattern, but it is a solution for a problem that came into being by combining several complimentary patterns.

A few years after I created the data portal, various other design patterns were formalized that describe other solutions to this same problem space. Some are similar, some are not. If you look into each solution, it is clear that each one is actually a different combination of some lower level design patterns, working together to solve the problem.

The thing is, every pattern your bring into your solution (or ever pattern brought in by a higher level pattern) comes with its own consequences. You need to be careful to minimize the negative consequences of all those patterns so the overall balance is toward the positive.

**In short: don’t be afraid to combine simple or basic design patterns together to solve a bigger problem, but be aware of the negative consequences of every pattern you bring into play.**

Having introduced this concept of “low level” vs “high level” patterns, I’m going to follow that a bit further. Most of the patterns in the original GoF book are what I’d call low level patterns. They stand alone and have little or no dependency on each other. Each one solves a very narrow and clear problem and has very clear good/bad consequences.

Of course that was 15 years ago, and since then people have applied the pattern concept to more complex and bigger problem spaces. The resulting solutions (patterns) very often build on other patterns. In other words we’re raising the level of abstraction by building on previous abstractions. And that’s a fine thing.

But it is really important to understand that ultimately patterns are implemented, and the implementations of patterns are often far messier than the abstract though models provided by the patterns themselves. Even that is OK, but there’s a meta-consequence the flows out of this: complexity.

As you start to use higher level patterns, *and their implementations*, you can easily become locked into not only the implementation of the pattern you wanted, but also the implementations of the lower level patterns on which the implementation is built.

Again I’ll use IoC to illustrate my point. If you want IoC you’ll almost certainly use a pre-existing implementation. And once you pick that framework, you are stuck with it. You won’t want to use more than one IoC framework, because then you’d have multiple containers, each configured differently and each competing for the attention of every developer. The result is a massive increase in complexity, which means a reduction in maintainability and a corresponding increase in cost.

Now suppose you pick some higher level pattern, perhaps a portal or gateway, that is implemented using IoC. If you want the implementation of the gateway pattern you must also accept a dependency on *their IoC framework choice*.

People often ask me whether (or when will) CSLA .NET will incorporate Enterprise Library, log4net, Unity, Castle/Windsor, &lt;insert your framework here&gt;. I try very, very, very hard to avoid any such dependencies, because as soon as I pick any one of these, I make life really hard for everyone out there who didn’t choose that other framework.

CSLA 3.8 has a dependency on a simple data structure framework, and even that was a continual nightmare. I can hardly express how happy I am that I was able to get rid of that dependency for CSLA 4. Not that the data structure framework was bad – it does a great job – but the complexity introduced by the dependency was just nasty.

**In short: be aware of the complexity introduced as high level patterns force you to accept dependencies on lower level patterns and implementations.**

The final topic I’d like to cover flows from a conversation I had with Ward Cunningham a few years ago. We were talking about patterns and the “pattern movement”, and how it has become a little warped over time as people actively look for ways to apply patterns, rather than the patterns being used because they are the natural answer to a problem.

It is kind of like a carpenter who spends a lot of money buying some really nice new power tool. And then trying to use that power tool for every part of the construction process – even if that means being less efficient or increasing the complexity of the job – just to use the tool.

Obviously I’d never want to hire such a carpenter to work on my house!!

Yet I’ve seen developers and architects get so fascinated by specific patterns, frameworks or technologies that they do exactly that: increase the complexity of simple problem domains specifically so they can use their new toy concept.

In this conversation Ward suggested that there are different levels of understanding or mastery of patterns. At the most basic level are people just learning what patterns are, followed by people who “get” a pattern and actively seek opportunities to use that pattern. But at higher levels of mastery are people who just do their job and (often without a conscious thought) apply patterns as necessary.

Carpenters don’t think twice about when and how to construct a staircase or put together a 2x6” wall frame. These are common design patterns, but they are natural solutions to common problems.

**In short: strive for “pattern mastery” where you are not fixated on the pattern, but instead are just solving problems with natural solutions, such that the pattern “disappears” into the fabric of the overall solution.**

The pattern movement has been going on for at least 15 years in our industry. And over that time I think it has been far more beneficial than destructive.

But that doesn’t mean (especially as a consultant) that you don’t walk into many organizations and see horrible misuse of design patterns – the results being higher complexity, lower maintainability and higher cost of development and maintenance.

I think it is important that we continually strive to make patterns be a common abstract language for complex problems and solutions. And I think it is important that we continually educate *everyone* on development teams about the patterns and implementations we bring into our applications.

But most importantly, I think we need to always make conscious choices, not choices based on trends or fads or because somebody on the team is in love with pattern X or framework Y or technology Z.

1. Use a pattern because you have the problem it solves
2. Only use a pattern if the good consequences outweigh the bad (and remember that *every* pattern has negative consequences)
3. Use patterns and implementations only if the entire team understands them
4. Use the simplest pattern that solves your problem
5. Don’t be afraid to combine several simple patterns to solve a complex problem
6. Be aware of (and consciously accept) the consequences of any low level patterns that come with most high level pattern implementations
7. Strive for “pattern mastery”, where you are solving problems with natural solutions, not looking for ways to apply any specific pattern


Eventually maybe we’ll all be in a software development retirement home and we can shout things like “Memento” and “Channel adaptor” and everyone will chuckle with fond memories of how those patterns made our lives easier as we built the software on which the world runs.
