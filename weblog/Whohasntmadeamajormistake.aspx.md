---
title: Who hasn't made a major mistake?
postDate: 2017-06-04T14:39:38-05:00
abstract: 
postStatus: publish
---
04 June 2017

I read [this thread on reddit](https://np.reddit.com/r/cscareerquestions/comments/6ez8ag/accidentally_destroyed_production_database_on/) thanks to [terrajobst](https://twitter.com/terrajobst) - with some amazement, and empathy.

Perhaps most people haven't made a major mistake in their careers, but I've made more than one. And *my* mistakes were probably more directly my fault than the mistake this poor person make - a mistake that was clearly caused by poor practices by the employer, not be the fresh-out-of-college employee.

I'll summarize what I believe are the two worst mistakes I've made.

Major mistake one was about eight months into my first real job out of university. This predated the concepts of source control like we know it now, so we all worked on a common directory structure that contained the source code for *everything*. And I deleted it all.

Yup, thought I was deleting something else, but did a recursive delete of the entire source code directory structure, instantly bringing all our developers to a full stop and losing a day's work (or more if the backups weren't good).

Fortunately the backups *were* good, thanks to a competent system administrator who not only performed the backups, but also regularly tested them. Yeah, just because you "have a backup" means nothing unless your regular IT process includes testing the restore process.

My mistake essentially cost all developers at least two days of time. The day lost when I deleted their work, some hours for the restore, and then another day for everyone to *redo* their work.

Still, I didn't get fired, though I did get a lot of crap from my colleagues and was on management's sh\*t list for a while. And rightly so in my view.

This is probably a bit arrogant, but I strongly suspect I got to keep my job because I was a young hot-shot with no kids, and really no life to speak of, so my productivity as a developer was the best on our entire team. Except probably for my boss, who was an *amazing* developer!

Major mistake number two was about three years into my career (working at my second real job after university). I worked in IT and had (temporarily) left software development to become the system administrator and manager of the help desk.

I thought our security policies were too lax, and I'd been researching how to tighten up the rules around who had which kind of network and system permissions. Unfortunately what I *didn't* know was that changing these policies would invalidate everyone's password. Nor did I have the wisdom to do this over a weekend or anything - so I made the change midday.

Next thing you know, a few hundred people lost access to the entire computer system, basically bringing the entire bio-medical manufacturing company to a halt.

Sweating profusely, with basically every manager in the company breathing down my neck, I wrote a script to reset all passwords to a known value so it was possible to get everyone back online.

Basically I cost the company a half day's work, and I'm sure people had to work overtime to catch up and meet deadlines for products to be delivered to customers on time.

Yet again, my f\*ckup to be sure. Fortunately I'd been there for quite some time and had built up non-trivial personal capital - all of which was probably spent in that one brief moment when I pressed `enter` on the line that accidentally locked everyone out of the system.

I read through that reddit post from the poor junior dev, apparently just following flawed onboarding instructions. I suppose the end result of that mistake is comparable to mine, and they had no personal capital to spend (this being day one on the job).

Regardless, from the poster's account it is *so* clear that the mistake was absolutely the responsibility of the employer - flawed onboarding instructions, extremely shoddy separation between dev and prod environments, apparently no regular testing of backups to make sure they could restore. The sort of environment I experienced back in the 1980's - and wouldn't expect to see anywhere *today*!

In my view the poster on reddit shouldn't have lost their job like that. They probably should get a lot of crap from coworkers, and perhaps go down in company history as the person who accidentally instigated better processes for development and IT. But not job loss.

On the other hand, perhaps this is for the best - a place run so poorly perhaps isn't a great start to anyone's career. Just think of all the bad habits a new employee might pick up working in a place like that.
