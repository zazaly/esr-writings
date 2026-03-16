::: {#Header}
  ------------------------- --
  Samizdat: Stinks on Ice   
  ------------------------- --
:::

::: {#Menu}

------------------------------------------------------------------------

[Home Page](http://www.catb.org/~esr "My home page")\
[What\'s New](http://www.catb.org/~esr/whatsnew.html "What's new on this site")\
[Site Map](http://www.catb.org/~esr/sitemap.html "Map of the site")\
[Software](http://www.catb.org/~esr/software.html "Software I maintain")\
[Projects](http://www.catb.org/~esr/projects.html "My projects")\
[HOWTOs](http://www.catb.org/~esr/faqs/ "My FAQ documents")\
[Essays](index.html "Essays and ruminations")\
[Personal](http://www.catb.org/~esr/personal.html "Portrait of the author")\
[Weblog](http://www.ibiblio.org/esrblog/)\
[Freedom!](http://www.catb.org/~esr/netfreedom/)\
[Firearms!](http://www.catb.org/~esr/guns/)\

------------------------------------------------------------------------
:::

::::: {#Content}
::: annotation
On Monday, 24 May 2004 I found the following note in my inbox:

    Justin Orndorff :
    > Attached is an upcoming book to be put out by the
    > Alexis de Tocqueville Institution (www.adti.net). If
    > you're receiving this mail then we've probably been in
    > touch before now, regarding our research.
    > 
    > Questions / comments / concerns should be directed to
    > Ken Brown -  kenbrown@adti.net
    > 
    > Have a great weekend,
    > Justin Orndorff

Attached to it was a 92-page PDF that described itself as excerpts from Samizdat: And Other Issues Regarding the \`Source\' of Open Source Code.

This had to be the tome promised to us in a press release ten days previously, titled [Torvalds claim to \"invent\" Linux probably false, says new study](http://www.adti.net/kenarbeit/samiz.release.html). ADTI\'s claims had already been addressed with [withering sarcasm](http://www.linuxworld.com/story/44851.htm) by Linus Torvalds and [blasted](http://www.cs.vu.nl/~ast/brown/) by Andy Tanenbaum, the man from whom ADTI alleges that Linus stole Linux.

I found the fact that it had been sent to me rather curious, for I have no recollection of ever having had dealings with ADTI. Nor did anything in my back mail suggest that I had ever been queried by them. But I give a lot of interviews, and it is at least possible I might have forgotten one.

The following, marked up for HTML and with a few typos fixed, is the response I sent back less than an hour later. A few further notes follow it.
:::

------------------------------------------------------------------------

Judging by these excerpts, this book is a disaster. Many of the claimed facts are bogus, the logic is shoddy, some of the people you claim to have used as important sources have already blasted you for inaccuracy, and at the end of the day you will have earned nothing but ridicule for it.

I\'m going to be charitable and assume that this mess is the result of honest error (rather than, as some are now charging, a paid hatchet job). Accordingly, I suggest some corrections here. Be aware that I *will* publish this critique if I am not swiftly convinced that those corrections will be incorporated.

The problems start in the abstract. Software is not composed of interchangeable parts that can be hodded from one project to another like a load of bricks. Context and interfaces are everything; unless it has been packaged into a library specifically *intended to move*, moving software between projects is more like an organ transplant, with utmost care needed to resect vessels and nerves. The kind of massive theft you are implying is not just contingently rare, it is necessarily rare because it is next to impossible.

I have been part of the hacker community for more than 25 years now and am one of its most expert historians. If we were in the habit of stealing code, I would *know* --- and I would blow the whistle, because I am a libertarian who believes in strong IP rights.

Your claim that we know nothing about the origins of most of what you call \"hybrid\" code is false. We use version-control systems; many projects have change logs clear back to the single empty file they started with. These histories can be tracked, and changes attributed to individuals.

I am willing to publish all my change logs and delta sequences so that anyone in the world can see how my projects evolved from their beginnings. Is Microsoft or Oracle or Computer Associates willing to do likewise?

Your claim that we know the origins of proprietary code is also false. We don\'t, because it is not published.

That a piece of code came from a proprietary vendor is no guarantee that it originated there. Proprietary outfits lift code from elsewhere all the time. It is known from behavioral analysis of the Microsoft TCP/IP stack, for example, that they swiped their code from BSD. So there may well be be immense amounts of stolen IP in proprietary code, hidden by commercial secrecy. Who can know?

We in the open-source world are accountable. We have audit trails. We have nothing to hide, and we prove it by publishing everything we do where the world can see it. Can proprietary vendors say the same?

Your account of the legal disclosure history of the Unix source code is seriously wrong. Persons authorized by AT&T *did*, in fact, frequently ship source tapes which contained no copyright notices --- I know, because I still have some of that source code. Therefore, under the pre-1989 publication doctrine, it is seriously questionable whether AT&T retained copyright at all. (In 1993, the federal judge in the AT&T vs. BSD case recognized this fact in a finding that put pressure on AT&T to settle.)

Furthermore, from a very early stage those tapes contained material contributed by others in academia and various non-AT&T labs. AT&T may not even have had legal rights to distribute this code, and certainly had no ethical right to distribute it except as part of the commons which all parties understood they were co-developing.

Both these things were already true when the Lions book leaked. This is why the the Unix developers *at Bell Labs itself* approved of the book --- they saw it not as theft from them but as a sign of healthy community, and knew perfectly well they were getting back huge amounts of value from outside contributors.

Your description of the supposed \"three factions\" is also wrong, I can tell because I don\'t fit in any of them, nor do any of my peers with which I have discussed these issues.

In fact, *all* hackers condemn IP theft --- this is what distinguishes us from the cracker/phreak subculture. Even the FSF faction that thinks proprietary code is evil has repeatedly and publicly condemned piracy and stealing other peoples\' code. They want to destroy the proprietary system, but they insist on doing it by their own efforts, not by theft.

Really, there are only two factions. One says \"Theft is wrong. Proprietary software is also wrong. Don\'t do either.\" The other, which I belong to, says \"Theft is wrong. Proprietary software is mostly crap. Therefore, we don\'t need to either steal it or condemn it as wrong, just write better code.\"

Linus Torvalds and Andy Tanenbaum have both rejected your storyline that Linux is a derivative of Minix. Even if you suppose Torvalds is lying, the fact that Tanenbaum (the wronged party in your narrative) has condemned you in public for inaccuracy and distortions should tell you something.

If the inventor of Minix agrees with the inventor of Linux that Linux is not a derivative work of Minix, who are *you* to claim otherwise?

(Relying on Bezroukov\'s account was a bad mistake. The man is a [crank and an idiot](response-to-bezroukov.html).)

You claim that \"To date no other product comes to life in this way\", presenting Linux as a unique event that requires exceptional explanations. This is wrong. Many other open-source projects of the order of complexity of the early Linux kernel predated it; the BSD Unixes, for example, or the Emacs editor. Torvalds was operating within an established tradition with well-developed expectations.

\"Is it possible that building a Unix operating system really only takes a few months ---and, oh by the way, you don\'t even need the source code to do it?\" Yes, it is possible, because there are published interface standards. I might have done it myself if it had occurred to me to try --- in fact, I have sometimes wondered why it didn\'t occur to me.

As for whether it was possible to produce Linux in the amount of time involved --- it is never wise to assume that genius programmers cannot do something because the incompetent or mediocre cannot. Especially when, as in Linus\'s case, the genius already has a clear interface description and a mental model of what he needs to accomplish.

As to Fred van Kempen\'s claim that I did not know what I was talking about when I described Linus\'s inventive process, be aware that Linus reviewed and endorsed my paper before publication in 1997. So Van Kempen\'s claim is not just that I\'m wrong but that Linus has his own history wrong.

How dare you first use Richard Stallman\'s inability to make the HURD work as an implicit argument that Linus must have stolen code, and then quote Stallman as saying \"I never wrote any code for the Hurd myself\"? This argument at least verges on dishonesty.

I can tell you exactly why the HURD tanked. It was listening to a presentation by HURD\'s project lead in 1996, and realizing the project was doomed, that started me on the train of thought that led to \"The Cathedral and the Bazaar\". They were trying to do engineering and pure R&D at the same time; they lacked focus or any drive to actually ship code; and their development group was too small and inbred.

You propose that the absence of credits to developing countries might be evidence of some sinister memory-hole effect. The true explanation is much simpler: developing countries don\'t have Internet. There is a straight-up geographical correlation between contributions to open-source projects and Internet penetration.

Torvalds\'s ambiguity about \"GNU/Linux\" in 2001 was not complicated; he dislikes the term rather strongly but was at the time reluctant to get into a political scrap with Stallman, whom he personally dislikes. The dislike has since hardened and become sufficiently public that I am not betraying a confidence by writing this.

Your discussion of copying and reverse-engineering is a pile of innuendo without facts. Though reverse engineering is legal in black-letter law, you write about it as though it were a crime that open-source developers should not be getting away with.

In your discussion of obfuscation software, I hope it is simple ignorance rather than intentional deceit that prevents you from noting that open-source code has *none* of the characteristics of obfuscated code, and that obfuscators are therefore *irrelevant* to the question you are supposedly addressing.

Pretty printers do not in fact remove the evidence of copying that is most telling to a programmer --- that is, use of identical control flow and data structures in circumstances where the second programmer had wide discretion to do things in a different way.

\"Corporate interests cannot fund truly free software because their interests are tied to the promotion of their business.\" This is not only false in theory but falsified in practice. Apache, which you specify as an example of \"truly free\" is funded by a consortium of corporations.

On to economics\...

You claim that \"The commercial open source model is \[\...\] depreciating the value of U.S. proprietary software.\" This is economically illiterate. What\'s being depressed is not the value, but the price the market will bear. As I demonstrated in \"The Magic Cauldron\", the value of software as an intermediate good (that is, its value as a productivity multiplier) is uncorrelated with market price.

What is actually being \"depressed\" here is the ability of proprietary companies to collect secrecy rent. But rent is not value --- in fact, the market and consumers benefit when rents are competed out of the system.

The \"investment\" in intellectual property that is being lost is a sunk cost, what technology investors call NRE or Non-Recoverable Engineering cost. It was gone anyway when it was spent.

Your advocacy of government funding for what you call \"true\" open source clashes oddly with your expessed concern about destroying IP rents and investment incentives. If I release a program that outcompetes and undercuts a proprietary vendor and discourages future investment in that application area, that effect will be independent of whether the license is GPL or BSD. Furthermore, if I have stolen code to build it, the loss and crime is no less if I BSDed the result rather than GPLing it.

Given the gravamen of your argument, I see no reason that you should condemn \"hybrid\" code but endorse \"truly free\" code --- unless, as some are now charging, ADTI is a Microsoft sock puppet and the actual goal is to neuter the open-source community so that it becomes nothing but an unpaid development arm for proprietary companies. I do not want to believe this, and hope you can supply some less sinister explanation.

In sum, if this excerpt is representative, your book is unpublishably bad. Fix it or bury it.

------------------------------------------------------------------------

::: annotation
I then waited three days for a response or even a simple acknowledgment. I did not get one. Here, then, are a few more comments following a second look:
:::

Anyone who thinks I sound harshly critical in the above should be be warned that the Samizdat excerpts are actually quite a bit lower in quality than my response suggests --- I was actually being relatively nice about the thing on the long odds that the ADTI people are honest and might be willing to correct the errors. But it was not to be.

The excerpts make it clear that this book is going to be a steaming pile of crap, full of anti-factual distortions, scare-mongering, and FUD. I haven\'t seen a book quite so egregiously shoddy and dishonest since Michael Bellesisles\'s Arming America. The good news is that, unlike Arming America, this book is so *obviously* bad that it is not likely to persuade anyone of its conclusions who isn\'t already zealously on the author\'s side.

I began reading the excerpts skeptical of the widespread conspiracy theory that this book is a paid hatchet job commissioned by Microsoft. Now I find this theory much more credible. I can\'t imagine how anyone would want their names on a disgrace like this unless they were getting paid extremely well for undergoing the humiliation.

P.S.: Some readers have pointed out that my language above was unclear in one respect. It is perfectly legal for Microsoft to have lifted code from BSD. But we only know about this by looking at the responses to certain odd TCP/IP packets. The responses are underspecified in the standard, and it is possible to build family trees of code derivation through behavioral analysis.

The point is this: Microsoft (legally) took BSD code, and the only way we know about it is through behavioural analysis. So how do we know other proprietary outfits haven\'t taken code illegally?
:::::

------------------------------------------------------------------------
