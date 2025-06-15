---
title: "Shirky: Situated Software"
source: "https://gwern.net/doc/technology/2004-03-30-shirky-situatedsoftware.html"
author:
  - "[[Clay Shirky]]"
published:
created: 2025-06-11
description: "Clay Shirky's writings about the Internet, including Economics and Culture, Media and Community, Open Source"
tags:
  - "clippings"
---
### Situated Software

I teach at NYU's Interactive Telecommunications Program (ITP), where the student population is about evenly divided between technologists who care about aesthetics and artists who aren't afraid of machines, which makes it a pretty good place to see the future.

Part of the future I believe I'm seeing is a change in the software ecosystem which, for the moment, I'm calling situated software. This is software designed in and for a particular social situation or context. This way of making software is in contrast with what I'll call the Web School (the paradigm I learned to program in), where scalability, generality, and completeness were the key virtues.

I see my students cheerfully ignoring Web School practices and yet making interesting work, a fact that has given me persistent cognitive dissonance for a year, so I want to describe the pattern here, even in its nascent stages, to see if other people are seeing the same thing elsewhere.

**Users By The Dozens**

We've always had a tension between enterprise design practices and a "small pieces, loosely joined" way of making software, to use David Weinberger's felicitous phrase. The advantages to the latter are in part described in [Worse is Better](https://web.archive.org/web/20151222035833/http://www.jwz.org/doc/worse-is-better.html) and [The Cathedral and the Bazaar](https://web.archive.org/web/20151222035833/http://www.firstmonday.dk/issues/issue3_3/raymond/). Situated software is in the small pieces category, with the following additional characteristic -- it is designed for use by a specific social group, rather than for a generic set of "users".

The biggest difference this creates relative to classic web applications is that it becomes easy to build applications to be used by dozens of users, an absurd target population in current design practice. Making form-fit software for a small group of users has typically been the province of banks and research labs -- because of the costs involved, Web School applications have concentrated on getting large-scale audiences. And by privileging the value that comes with scale, Web School applications put other kinds of value, particularly social value, out of reach.

We've been killing conversations about software with "That won't scale" for so long we've forgotten that scaling problems aren't inherently fatal. The N-squared problem is only a problem if N is large, and in social situations, N is usually not large. A reading group works better with 5 members than 15; a seminar works better with 15 than 25, much less 50, and so on.

This in turn gives software form-fit to a particular group a number of desirable characteristics -- it's cheaper and faster to build, has fewer issues of scalability, and likelier uptake by its target users. It also has several obvious downsides, including less likelihood of use outside its original environment, greater brittleness if it is later called on to handle larger groups, and a potentially shorter lifespan.

I see my students making some of these tradeoffs, though, because the kinds of scarcities the Web School was meant to address -- the expense of adequate hardware, the rarity of programming talent, and the sparse distribution of potential users -- are no longer the constraints they once were.

**Teachers on the Run**

The first inkling I got that the Web School rationale might be weakening was an application written by two of my former students, Paul Berry and Keren Merimeh. In November of 2002, as a project for a class on the feeling of online spaces called Social Weather, they created an application called (alarmingly) Teachers on the Run.

Teachers on the Run was essentially HotorNot for ITP professors, to allow students to describe and rate us in advance of spring course registration. Every professor was listed in a database; students could come by anonymously and either enter a comment about a professor or cast a vote agreeing or disagreeing with an earlier comment. The descriptions were sorted in vote total order, so that a +5 description (5 more students had agreed than disagreed) was displayed higher than a +2 or a -3. And that was it -- a list of names, a list of comments, click to vote, and a simple sorting algorithm.

They launched it on a Friday. By Saturday night, another student called me at home to tell me I'd better take a look at it. There are only 200 or so students at ITP, but Teachers on the Run had already accumulated hundreds of comments, most positive, some negative, a few potentially libelous. More importantly, though, there had been over a thousand votes in 24 hours. By Monday morning, I had students telling me they knew what was on the site, not because they'd seen it, but because it had been the only topic of conversation over the weekend.

The curious thing to me about Teachers on the Run was that it worked where the Web School version failed. RateMyProfessors.com has been available for years, with a feature set that put the simplistic write/read/vote capabilities of Teachers on the Run to shame. Yet no one at ITP had ever bothered to use RateMyProfessors.com, though the weekend's orgy of rating and voting demonstrated untapped demand.

Despite the social energy it unleashed, I missed the importance of Teachers on the Run. I told myself that it had succeeded for a number of reasons that were vaguely unfair: The users knew the programmers; the names database had been populated in advance; the programmers could use the in-house mailing list to launch the application rather than trying to get attention through press releases and banner ads. Most damning of all, it wouldn't scale, the *sine qua non* of successful Web applications. DOA, QED.

Then I saw the design process my most recent class went through.

**The Class**

In a class called Social Software, which I taught last fall, the students worked in small groups to design and launch software to support some form of group interaction. To anchor the class, I required that whatever project they came up with be used by other ITP students. This first order benefits of this strategy were simple: the designers came from the same population as the users, and could thus treat their own instincts as valid; beta-testers could be recruited by walking down the hall; and it kept people from grandiose "boil the ocean" attempts.

What I hadn't anticipated was the second-order benefits. Time and again the groups came up against problems that they solved in part by taking advantage of social infrastructure or context-sensitive information that wouldn't be available to adherents of the Web School. Two strategies in particular stand out.

The first had to do with reputation systems. One project, The Orderer (designed by Vena Chitturi, Fa-yi Chou, Rachel Fishman, and Cindy Yang) was for coordinating group restaurant orders, common in late-night work sessions. The other, WeBe (Brandon Brown, Yoonjung Kim, Olivier Massot, Megan Phalines) was a tool for coordinating group purchases of things like chips or motors. Because money was involved, a Web School approach would require some way of dealing with the threat of non-payment, using things like pre-pay or escrow accounts, or formal reputation systems.

Instead, in both projects the students decided that since all the users were part of the ITP community, they would simply make it easy to track the deadbeats, with the threat of public broadcast of their names. The possibility of being shamed in front of the community became part of the application design, even though the community and the putative shame were outside the framework of the application itself.

**Communal Attention**

The other strategy had to do with communal attention. Two other projects, Scout (Karen Bonna, Christine Brumback, Dennis Crowley, Alex Rainert) and CoDeck (Mark Argo, Dan Melinger, Shawn Van Every, Ahmi Wolf) ended up being situated in the community in a more literal fashion. Scout indicates physical presence, by allowing students to register themselves as being present somewhere on the ITP floor, and displaying that information. CoDeck is a community-based video server, designed to allow video artists to share and comment on each other's work.

Both groups had the classic problem of notification -- getting a user to tune in requires interrupting their current activity, not something users have been known to relish. Billions were spent on Web School applications that assumed users would bookmark for a return visit, or would happily accept email alerts, but despite a few well-publicized successes like Schwab.com and eBay, users have mostly refused to "check back often."

Both Scout and CoDeck hit on the same solution: take most of the interface off the PC's dislocated screen, and move it into a physical object in the lounge, the meeting place/dining room/foosball emporium in the center of the ITP floor. Scout and CoDeck each built kiosks in the lounge with physical interfaces in lieu of keyboard/mouse interaction. Scout used a bar code reader to swipe in; CoDeck gutted a mid-70's BetaMax chassis and put a Linux machine inside, then used the BetaMax buttons to let the user control the video stream. Both Scout and CoDeck have web sites where users can enter or retrieve data, but the core piece of each is location in physical space that puts the application in a social context.

These projects all took the course's original dictum -- the application must be useful to the community -- and began to work with its corollary as well -- the community must be useful to the application.

**Group Capabilities**

We constantly rely on the cognitive capabilities of individuals in software design -- we assume a user can associate the mouse with the cursor, or that icons will be informative. We rarely rely on the cognitive capabilities of groups, however, though we rely on those capabilities in the real world all the time.

In brainstorming sessions, a group can generate not just more ideas but more kinds of ideas than the same individuals working in isolation, and a group consensus is often more accurate than the guess of the group's most knowledgeable individual. Groups also know a lot about themselves. People in work groups know who to go to for design advice, or who is unreliable in a pinch, without any formal designation of those roles. Members of social groups know who it's fun to go drinking with or who you shouldn't lend money to (often the same person) without needing that knowledge to be spelled out in a FAQ.

Web School software ignores this kind of knowledge, because it is hard to make explicit. On most large mailing lists, for example, only a handful of posters start discussions, while most posters simply follow-up; and, at a higher level, only a handful of the members post at all, while a most simply lurk. We've known about these patterns for decades, but mailing list software still does not offer any features specific to starting vs. continuing threads, nor does it treat high-volume posters and lurkers differently.

There is another strategy, however, analogous to asking the user to recognizing icons; the designer can simply assume the group has a certain capability, without needing to recapitulate it in code. If you have an uncollected payment in a communal buying pool, the software can kick out a message that says "Deadbeat alert. Deal with it." A real world group will have some way of handling the problem, usually through moral suasion or the threat of lost reputational capital, or even, in extreme cases, ostracism.

This is no different than what happens in offline groups every day, but the solution feels wrong, in Web School terms, because those web applications can't assume there is a tacit reputation system. By relying on existing social fabric, situated software is guaranteed not to work at the scale Web School apps do, but for the same reason, it can work in ways Web School software can't.

**Outside Eyes**

I finally started regarding situated software as a practical development strategy, rather than as a degenerate case of "real" application development, when I invited outside reviewers into the Social Software class for a mid-term critique. These were all people who work with social software for a living, and the critique session was enormously valuable. Two of the recommendations made by the reviewers, however, struck me funny.

The first was the suggestion, made to the CoDeck group, that they should make all the features of their video tool available over the web -- upload, download, comment, and so on. The second recommendation was an exhortation to the WeBe group that they should look at Web School group-buying sites like Mercata and MobShop as guides to their own work.

This was the moment for me when cognitive dissonance finally became unsupportable. Each of those comments was a) exactly what I would have said, had I been an outside reviewer in someone else's class, and b) obviously wrong, given the problem the respective groups were attacking.

The suggestion about general web accessibility for the CoDeck interface came in the form of a rhetorical question -- "Why not make it as broadly accessible as possible?" In the Web School, of course, the answer is "No reason", since more users are always A Good Thing, but for CoDeck there were several good reasons for not simply turning their project into a Web video app.

First, the physicalization of the interface, using the gutted BetaMax deck, provides a communal affordance that it is impossible to replicate over the web. Second, since CoDeck serves a tight community, the density of communication among ITP video makers would be diluted by general accessibility. Third, having the video deck in the lounge makes it self-policing; the cohesion of the community keeps it largely free from abuse, whereas a generally accessible and password-free "upload and critique" video site would become a cesspool of porn within hours. Finally, serving a local community maximizes use of free bandwidth on the local network, enabling features that would saddle a public system with crippling costs.

**WeBe Small**

Similarly, the recommendation that WeBe should look at Mercata and MobShop carried with it the assumption that the goal should eventually be to operate at large scale. However, Mercata and MobShop failed because they were built to scale.

Those sites required a virtuous circle, where more users meant more savings meant more users. Alas, the thought that somewhere, someone else was saving a bundle on Tupperware was never enough to attract users, and without critical mass, the virtuous circle turned vicious. Like RateMyProfessors.com, the mere existence of a Web School app wasn't enough, and having been built for tens of thousands of users, it couldn't operate for dozens or even hundreds.

WeBe, on the other hand, was copying a small-scale pattern they first observed when a fellow student, Scott Fitzgerald, orchestrated a 30-license discount purchase of Max, the multi-media editing software. He used the ITP mailing list to recruit buyers, and then walked around the floor twisting arms and collecting checks. This required real social fabric to work -- everyone knew and trusted Scott.

As the instigator, Scott also benefited from the good karma -- everyone who participated saved quite a bit of money, enhancing his reputation. Unlike actual capital, reputational capital is easier to accumulate in smaller and more closed social systems. The idea for WeBe came about in part because Scott said the purchase, though successful, had required too much work. Whatever the WeBe group could do to make ITP group purchases easier, they didn't need to build identity or reputation systems. Because the software was situated in a particular (and particularly tight) community, they got those things for free.

**Old Scarcities Fade Away**

Where the Web School works well, it works because it is the right kind of response to some sort of scarcity. There's scarcity of funds: Servers are expensive, not to mention load-balancing routers, tape backups, and the other accouterments of serious uptime. There's scarcity of talent: Good programmers are hard to find; great programmers are scarce as hen's teeth. And there's scarcity of use: Users are busy, they are creatures of habit, and there is significant competition for their attention.

However, addressing these scarcities can give Web School design a kind of merry-go-round quality. You need to scale because building a useful web application is so expensive, but much of the expense comes from the requirements of scale. Furthermore, these scarcities amplify one another: You need a big hardware budget to build an application that can scale, but you need good programmers and system administrators to handle the load, whose salaries require an increased marketing budget, to attract enough users to pay for it all.

What I think I'm seeing my students do is get off that ride. They can do this because none of the scarcities the Web School addresses are as significant as they used to be. First of all, Moore's Law and its equivalent for storage, plus the gradual improvement in operating systems, means that an $800 desktop machine can also be a pretty good server right out of the box.

Second, user attention was scarce in part because there were so few users at all. In the 90's, launching an application on the Web meant forgoing any direct connection with a particular real world community, because internet users were spread thin, and outside the IT industry, most real world groups had only a sub-set of members who were online.

Those days are ending, and in some places they are over already. In the US today, if you are under 35 or make over 35,000 dollars a year, you are probably online, and if both of those things are true, then most of the people you know are probably online as well. You can now launch an application for a real world group, confident that all of them will have access to the internet.

**The Nature of Programming, and the Curious Case of MySQL**

Finally, the practice of programming is changing. Gartner recently caused a stir by saying there would be 235,000 fewer programmers in the US ten years from now. This would have been like predicting in the 80s, that there would be fewer typists in the US by 2004. Such a prediction would be true in one sense -- the office typing pool has disappeared, and much data entry work has moved overseas. But actual typing, fingers hitting the keyboard, has not disappeared, it has spread everywhere.

So with programming; though all the attention is going to outsourcing, there's also a lot of downsourcing going on, the movement of programming from a job description to a more widely practiced skill. If by programmer we mean "people who write code" instead of "people who are paid to write code", the number of programmers is going to go up, way up, by 2015, even though many of the people using perl and JavaScript and Flash don't think of themselves as programmers.

A variety of technologies are driving this -- perl, PHP, ActionScript, DHTML -- with a lot of mixing and matching and no one core tool, with one curious exception. Every application of this pattern I've seen has used a MySQL database.

There's an analogy here with web server software. In the mid-90s, getting a web server running was such a messy endeavor that it was a project goal in and of itself. Then Apache came along, and so simplified the process that the web server became a simple building block for larger things.

MySQL does this for databases. This matters for the development of group applications, because the ability to sort is a public good. If Teachers on the Run had simply been a list of professors with attached comments, it would have been a write-only application, like those worthless "Tell us what you think!" comment forms on the bottom of news articles. One of the critical things any group wants to know is "What does everyone else think?", especially if there is reason to believe that the group in aggregate knows more than any individual. Adding the 'users rate comments' system, and then pulling the data out by rating instead of time, made the system valuable.

You can of course build these kind of features in other ways, but MySQL makes the job much easier, so much easier in fact that after MySQL, it becomes a different kind of job. There are complicated technical arguments for and against using MySQL vs. other databases, but none of those arguments matter anymore. For whatever reason, MySQL seems to be a core tool for this particular crop of new applications.

**Software for Your Mom**

Situated software isn't a technological strategy so much as an attitude about closeness of fit between software and its group of users, and a refusal to embrace scale, generality or completeness as unqualified virtues. Seen in this light, the obsession with personalization of Web School software is an apology for the obvious truth -- most web applications are impersonal by design, as they are built for a generic user. Allowing the user to customize the interface of a Web site might make it more useful, but it doesn't make it any more personal than the ATM putting your name on the screen while it spits out your money.

Situated software, by contrast, doesn't need to be personalized -- it is personal from its inception. Teachers on the Run worked this way. Everyone knew that Paul and Keren built it. You could only rate Clay and Marianne and Tom and the other ITP professors. You didn't even know it even existed unless you were on the ITP mailing list. The application's lack of generality or completeness, in other words, communicated something -- "We built this for you" -- that the impersonal facade of RateMyProfessors.com doesn't have and can't fake.

One of my students mentioned building a web application for his mother, a schoolteacher, to keep track of her class. If you were working alone, unpaid, and in your spare time, there's no way you could make an application that would satisfy the general and complete needs of schoolteachers everywhere. You could make one for your mom, though.

Small, purpose-built apps have always existed, of course -- learning BASIC used to be a rite of passage for PC owners, and data intensive institutions like investment banks and research labs write software for small groups of users. Now, though, the combination of good tools, talented users and the internet as a social stage makes the construction of such software simpler, the quality of the result better, and the delivery to the users as simple as clicking a link. The design center of a dozen users, so hard to serve in the past, may become normal practice.

**What Next?**

So what happens next? If what I'm seeing is not transitory or limited to a narrow set of situations, then we'll see a rise in these small form-fit applications. This will carry some obvious downsides, including tying the developers of such applications to community support roles, and shortening the useful lifespan of the software made in this way.

Expectations of longevity, though, are the temporal version of scale -- we assume applications should work for long periods in part because it costs so much to create them. Once it's cheap and easy to throw together an application, though, that rationale weakens. Businesses routinely ask teams of well-paid people to put hundreds of hours of work creating a single PowerPoint deck that will be looked at in a single meeting. The idea that software should be built for many users, or last for many years, are cultural assumptions not required by the software itself.

Indeed, as a matter of effect, most software built for large numbers of users or designed to last indefinitely fails at both goals anyway. Situated software is a way of saying "Most software gets only a few users for a short period; why not take advantage of designing with that in mind?"

This, strangely, is a kind of progress, not because situated software will replace other kinds of applications, but because it mostly won't. For all the value we get out of the current software ecosystem, it doesn't include getting an application built for a handful of users to use for a few months. Now, though, I think we're starting to see a new software niche, where communities get form-fit tools for very particular needs, tools that fail most previous test of design quality or success, but which nevertheless function well, because they are so well situated in the community that uses them.

---

*Thanks to Shawn Van Every for invaluable comments on an earlier draft of this piece.*