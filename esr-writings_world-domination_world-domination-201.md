::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.article lang="en"}
::::::::::::: titlepage
<div>

<div>

## []{#id247934}World Domination 201 {#world-domination-201 .title}

</div>

<div>

::::: authorgroup
::: author
### [Eric]{.firstname} [Steven]{.othername} [Raymond]{.surname} {#eric-steven-raymond .author}
:::

::: author
### [Rob]{.firstname} [Landley]{.surname} {#rob-landley .author}
:::
:::::

</div>

<div>

Copyright © 2006 Eric S. Raymond

</div>

<div>

Copyright © 2006 Rob Landley

</div>

<div>

::: revhistory
  **Revision History**                                                               
  --------------------------------------------------------------- ------------------ -----
  Revision 1.4                                                                       esr
  Clarification of the 64-bitness of Vista.                                          
  Revision 1.3                                                                       esr
  Knoppix hardware autodetect is based on kudzu, attribute it.                       
  Revision 1.2                                                    26 December 2006   esr
  Typo and spelling corrections.                                                     
  Revision 1.1                                                    13 November 2006   esr
  Reorganize, cite OSDL survey, and note Intel\'s recent moves.                      
  Revision 1.0                                                    5 July 2006        esr
  Initial version.                                                                   
:::

</div>

</div>

------------------------------------------------------------------------
:::::::::::::

::: toc
**Table of Contents**

[[Introduction](world-domination-201.html#id247954)]{.sect1}

[[Part 1: Why is 2008 a hard deadline?](world-domination-201.html#id248022)]{.sect1}

[[Punctuated Equilibrium: Stability through network effects.](world-domination-201.html#id248026)]{.sect2}

[[When do transitions happen?](world-domination-201.html#id248066)]{.sect2}

[[When does the new 64-bit platform arrive?](world-domination-201.html#id286667)]{.sect2}

[[What will the new 64 bit operating system be?](world-domination-201.html#id286734)]{.sect2}

[[How long will the new 64-bit platform last?](world-domination-201.html#id286760)]{.sect2}

[[Is 2008 a hard deadline?](world-domination-201.html#id286772)]{.sect2}

[[Part 2: Which operating system would win the 64-bit desktop today?](world-domination-201.html#id286821)]{.sect1}

[[The Contenders](world-domination-201.html#id286830)]{.sect2}

[[Windows x86-64](world-domination-201.html#id286841)]{.sect2}

[[Mac OS X](world-domination-201.html#id287020)]{.sect2}

[[Linux](world-domination-201.html#id287162)]{.sect2}

[[What will it take to win?](world-domination-201.html#id287267)]{.sect1}

[[Drivers For All Major Existing Hardware](world-domination-201.html#id287314)]{.sect2}

[[Legacy Platform Emulation.](world-domination-201.html#id287535)]{.sect2}

[[Surviving The Killer App.](world-domination-201.html#id287747)]{.sect2}

[[Enabling Preinstalls](world-domination-201.html#id287860)]{.sect2}

[[The Multimedia Perplex](world-domination-201.html#id288174)]{.sect2}

[[Facing The Music](world-domination-201.html#id288468)]{.sect1}

[[What Are The Alternatives?](world-domination-201.html#id288476)]{.sect2}

[[Codecs and the Competitive Minefield](world-domination-201.html#id288816)]{.sect2}

[[How Not To Do It](world-domination-201.html#id288870)]{.sect2}

[[Can Linspire save us?](world-domination-201.html#id288946)]{.sect2}

[[A. History Of The 8-to-16-to-32-bit Transitions](world-domination-201.html#history)]{.appendix}

[[B. The Microsoft Tax](world-domination-201.html#msoft)]{.appendix}
:::

:::::::: {.sect1 lang="en"}
::::: titlepage
<div>

<div>

## []{#id247954}Introduction {#introduction .title style="clear: both"}

</div>

</div>
:::::

:::: epigraph
Those who cannot learn from history are doomed to repeat it.

::: attribution
\--[George Santayana]{.attribution}
:::
::::

In the 1990s Linus Torvalds used to give a talk called *World Domination 101* on the early steps he believed Linux would need to take to achieve \"world domination --- fast\" ^\[[1](world-domination-201.html#ftn.id247976){#id247976}\]^. We\'ve made a lot of progress since then, but Linux desktop market share remains stuck below 5%, which is too low to garner support from hardware vendors in some critical areas like graphics and wireless hardware, and too small a political base from which to effectively oppose software patents, hardware DRM, and other horrors. For those within the Linux community, *World Domination 201* is about how to take advantage of an opportunity to go the rest of the way. For those outside it, this is a warning of what\'s coming if we fail.

When 8-bit microcomputer hardware stopped selling, it took 8 bit software down with it. The end of 16-bit hardware undid the dominance of DOS, and the end of 32-bit hardware spells the end of the road for Win-32. What will replace 32 bit Windows as the next dominant OS has yet to be decided.

The industry-wide switch to 64-bit hardware is opening a critical transition window during which the new dominant operating system will be determined. This window will close at the end of 2008, a hard deadline. The last such transition completed in 1990, the next one cannot be expected before 2050.

The three contenders for the new 64-bit standard are Windows-64, MacOS X, and Linux. The winner will be determined by desktop market share, the bulk of which consists of non-technical end users.

This paper tries to answer a number of questions: Why is 2008 a hard deadline? What is the current state of the three major contenders trying to become the new 64-bit standard? What are the major blocking issues to to each platform\'s desktop acceptance? What specific strategies and tactics can Linux use to cope with its most pressing problems? We close with a sober consideration of the costs of failure.
::::::::

::::::::::::::::::::::::::::::::::::::::::::::: {.sect1 lang="en"}
::::: titlepage
<div>

<div>

## []{#id248022}Part 1: Why is 2008 a hard deadline? {#part-1-why-is-2008-a-hard-deadline .title style="clear: both"}

</div>

</div>
:::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id248026}Punctuated Equilibrium: Stability through network effects. {#punctuated-equilibrium-stability-through-network-effects. .title}

</div>

</div>
:::::

Before establishing when transition periods occur, the first question to ask is why are there periods of stability between them? The answer is that network effects establish a standard.

Network effects cause the value of connected sets of nodes to grow faster than the linear increase in nodes (anywhere from n log(n) to n^2^). This allows even slightly larger networks to dominate, becoming \"the obvious choice\" for new installations and new product introductions, and eventually to take established market share from smaller networks. In a networked market, the largest player tends to get larger, and once past 50% market share usually continues up the s-curve to monopoly status.

Network effects in software, especially mass-market operating systems, make it highly advantageous to be using the same software as everyone else. Users buy the platform that offers the most content, and developers write content for the platform that has the most users. This positive feedback loop establishes a standard, and if that standard is owned it creates a natural monopoly.

Migrations en masse only overcome this entrenched stability when there is no alternative. The pattern is consistent since the beginning of the personal-computer industry in the mid-1970s: software platform transitions follow hardware platform transitions. Long periods of monopoly are interrupted by episodes of brief rapid change, in a pattern resembling the \"punctuated equilibrium\" of evolutionary biology. Historically, dominant operating systems have only lost their position by being tied to an obsolete hardware platform.^\[[2](world-domination-201.html#ftn.id248059){#id248059}\]^
::::::

::::::::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id248066}When do transitions happen? {#when-do-transitions-happen .title}

</div>

</div>
:::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id248070}Moore\'s Law {#moores-law .title}

</div>

</div>
:::::

Hardware platform transitions are determined by changes in the size of addressable memory, demand for which doubles every 18 months on a curve closely predicted by Moore\'s Law. For the past 30 years, the low end of retail \"desktop system\" memory has been about 2^((year-1975)/1.5)^ kilobytes, and the high end about 4 times that.^\[[3](world-domination-201.html#ftn.id248804){#id248804}\]^

Even after 30 years, Moore\'s Law continues to be predictive.^\[[4](world-domination-201.html#ftn.id248812){#id248812}\]^ It remains surprisingly accurate in part because memory and motherboard vendors schedule new product releases around it to avoid either falling behind the competition or cannibalizing the existing market prematurely.
::::::

::::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id248824}Learning from history. {#learning-from-history. .title}

</div>

</div>
:::::

The following table shows how much memory was sold preinstalled in new desktop personal computers over the past 30 years, including representative systems with dates of introduction (and in the case of hardware, the amount of memory that came \"standard\" with the system).

::: informaltable
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| Year                                                                                                                                                                                              | Low End | High End | Representative Systems                                                                                       |
+===================================================================================================================================================================================================+=========+==========+==============================================================================================================+
| 1975                                                                                                                                                                                              | 1K      | 4K       | Altair (Apr 1975: 1K)                                                                                        |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1978                                                                                                                                                                                              | 4K      | 16K      | Apple II (Jun 1977: 4K)                                                                                      |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1981                                                                                                                                                                                              | 16K     | 64K      | PC (Aug 1981: 16K), Commodore 64 (1982)                                                                      |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1984                                                                                                                                                                                              | 64K     | 256K     | Macintosh (Jan 1984: 128K), Amiga 1000 (1985: 256K)                                                          |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1987                                                                                                                                                                                              | 256K    | 1M       | Amiga 500 (1987: 512K), Compaq Deskpro, IBM PS/2                                                             |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1990                                                                                                                                                                                              | 1M      | 4M       | Windows 3.0 (1990) 3.1 (1992), Linux 0.01 (1991)^\[[a](world-domination-201.html#ftn.id248176){#id248176}\]^ |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1993                                                                                                                                                                                              | 4M      | 16M      | OS/2 3.0 (Nov 1994), Linux 1.0 (Mar 1994)                                                                    |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1996                                                                                                                                                                                              | 16M     | 64M      | Win 95 (Aug 1995), Linux 2.0 (Jun 1996)                                                                      |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 1999                                                                                                                                                                                              | 64M     | 256M     | Windows 2000 (Feb 2000), Windows XP (2001), Linux 2.2 (Jan 1999)                                             |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 2002                                                                                                                                                                                              | 256M    | 1G       | Linux 2.4 (Jan 2001), MacOS X (Mar 2001)                                                                     |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 2005                                                                                                                                                                                              | 1G      | 4G       | Linux 2.6 (Jan 2003), Win x86-64 (Apr 2005)                                                                  |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| 2008                                                                                                                                                                                              | 4G      | 16G      | The new 64-bit desktop.                                                                                      |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
| ::: footnote                                                                                                                                                                                      |         |          |                                                                                                              |
| ^\[[a](world-domination-201.html#id248176){#ftn.id248176}\]^ Footnote: Linus Torvalds had 4 megs in 1991, but implemented swapping to support people with 2 megabyte systems within a few months. |         |          |                                                                                                              |
| :::                                                                                                                                                                                               |         |          |                                                                                                              |
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+----------+--------------------------------------------------------------------------------------------------------------+
:::

Trend curves we can extract from this history enable us to make a fairly exact prediction of the length of desktop Linux\'s window of opportunity during the 32-bit-to-64-bit transition, and the length of the next equilibrium period after that.^\[[5](world-domination-201.html#ftn.id286509){#id286509}\]^

The decision points are where each CPU architecture has to be abandoned because it doesn\'t have enough memory. The high end moves 3 years before the low end (and the installed base tails off afterwards). Historically, during each transition the high end decides which new hardware platform the next standard will have, and arrival of the low entrenches a standard software platform for the life of that hardware.

When Moore\'s Law drives the memory demands of high end users beyond the memory capacity of the old hardware, early adopters have to start buying a whole new type of machine in order to access more memory. In doing so, they select which new platform starts a volume ramp-up and becomes cheaper and more widely deployed. When the old system\'s memory range hits the low end, the new type of hardware achieves sufficient sales volume to become as cheap or cheaper than the previous generation of hardware it replaces^\[[6](world-domination-201.html#ftn.id286529){#id286529}\]^. This drives the old hardware out of the market.
:::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id286539}Calibrating the table: the 8-bit and 16-bit eras {#calibrating-the-table-the-8-bit-and-16-bit-eras .title}

</div>

</div>
:::::

The 8-bit desktop lasted from 1975-1984, the 16-bit desktop from 1981-1990, and the 32-bit desktop from 1987-2008. This is because the 8-bit systems could access 64k of ram, the 16-bit systems could access 1 megabyte, and the 32-bit systems could access 4 gigabytes.

In 1975 the MITS Altair came with 1K of memory, but required 4K to run Microsoft Basic.^\[[7](world-domination-201.html#ftn.id286551){#id286551}\]^ In 1981, IBM introduced the IBM PC with a motherboard that would accept a minimum of 16k and a maximum of 64k of memory. In 1987, the Compaq Deskpro 386 beat IBM\'s PS/2 to market with the first 386 based PC, as 1 megabyte hit the high end highlighting the limit of 16-bit systems ^\[[8](world-domination-201.html#ftn.id286562){#id286562}\]^. These were the hardware platforms that launched each new generation.

The software platform for the 8-bit machines was BASIC. A version of BASIC was either burned into ROM or loaded from disk, and acted as the bootloader for any non-BASIC programs.^\[[9](world-domination-201.html#ftn.id286586){#id286586}\]^ BASIC was the lingua franca of the 8-bit world, with BASIC source code listings in all the computer magazines of the day (Byte, Compute, etc.), and even the original IBM PC had ROM BASIC as its default operating system. But in 1984, three years after the introduction of the new 16-bit hardware platform, the market for 8-bit systems running BASIC dried up and blew away as 64K fell off the low end of the demand curve. The installed base of 8-bit systems lasted for a few more years, but new sales and software development both tailed off suddenly and severely enough to oust Apple\'s Steve Jobs and Commodore\'s Jack Tramiel from the companies they had created.

The replacement for 8-bit BASIC was 16-bit DOS. Early on the PC had other operating systems (ROM-BASIC, CP/M-86, MP/M, Xenix) but DOS 2.0 in 1983 and 3.0 in 1984 gradually emerged as the new standard PC OS, and reduced the other competitors to irrelevance. DOS remained dominant until it too ran out of memory, at one megabyte.^\[[10](world-domination-201.html#ftn.id286603){#id286603}\]^
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id286612}The rise of Windows {#the-rise-of-windows .title}

</div>

</div>
:::::

Since Windows is the current 32-bit standard, its introduction deserves a closer look. New 32-bit hardware arrived when one megabyte hit the high end (1987), but not until three years later (1990) did 16-bit hardware fall off the low end, when DOS could no longer take full advantage of even the cheapest new machines.

Into this market vacuum Microsoft shipped Windows 3.0, an all but forgotten version that was not just unbelievably bad by modern standards but universally criticized at the time. But it succeeded because users were ready to abandon DOS for [*anything*]{.emphasis} that could use a larger address space.^\[[11](world-domination-201.html#ftn.id286630){#id286630}\]^

Windows 3.0 wasn\'t Microsoft\'s first attempt to replace DOS. Microsoft pushed OS/2 1.0 pretty hard circa 1988, and before that they\'d pushed Xenix hard circa 1983. In between they beat people over the head with Windows for years before anyone showed any interest, and Windows 3.0 was crap not just by modern standards but by the standards of the time. Once DOS was established as the standard, Microsoft [*itself*]{.emphasis} couldn\'t budge it until the hardware platform it ran on became obsolete.

Once the user base had migrated to the new standard it waited for that platform to incrementally improve over the next 5 years, despite a perceptible discontent prior to the release of Windows 95. In fact, once users were on the new standard, Microsoft again had trouble convincing them to upgrade from 3.1 to NT, or from Windows 98 to XP, despite compatible APIs. For over a decade now, the biggest competitor to each new release of Windows has been the installed base of previous versions of Windows.
::::::
:::::::::::::::::::::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id286667}When does the new 64-bit platform arrive? {#when-does-the-new-64-bit-platform-arrive .title}

</div>

</div>
:::::

According to the table, the 64-bit hardware standard arrived in 2005, and the 64-bit operating system arrives in 2008. The high end selects the hardware, the low end selects the operating system. When the high end encounters the old platform\'s memory limit they create a market for a new hardware platform, and when the old platform falls off the low end the market migrates to a new standard software platform.

The new 64-bit hardware standard did indeed arrive in 2005, when high end users first demanded more than 4 gigabytes or RAM in sufficient numbers for x86-64 systems to show up at retail outlets like Fry\'s.^\[[12](world-domination-201.html#ftn.id286682){#id286682}\]^ This hardware decision is already entrenched.

If the historical pattern repeats, three years after 64-bit hardware arrives, the market will adopt a new standard operating system. This places the obsolescence of the Win-32 API in 2008, because after 2008 even low-end systems will come standard with more than 4 gigabytes of memory, ruling out 32-bit processors with 32-bit operating systems for new purchases.^\[[13](world-domination-201.html#ftn.id286722){#id286722}\]^ Users demand an operating system that can use all the memory in their machine, and when every machine has more memory than the old operating system can access, users move to a new standard OS that can cope with more memory.
::::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id286734}What will the new 64 bit operating system be? {#what-will-the-new-64-bit-operating-system-be .title}

</div>

</div>
:::::

The three contenders are Windows-64, Linux, and MacOS X. The winner still could be any of them. Just as the hardware decision was uncertain in late 2003, the operating system remains is uncertain in late 2006.

As the new 64-bit systems hit the low end, the S-curve of 64-bit adoption will go close to vertical. This is the last chance to capture 50% market share, when the largest surge of new users decides upon a software platform to go with their new hardware. This doesn\'t mean a platform can wait until the last minute to get its act together, this is when the decision becomes irreversible. Network effects will already be strongly influencing adoption decisions when 64-bit \"crosses the chasm\" and acquires the high volume to be found at the low end. That will simply confirm the market\'s decision. It is already too late to introduce a new contender into the 64-bit race.

After the S-curve flattens out again, undecided new users will no longer be a significant influence on market share, and the largest platform will leverage its network effect advantage to consolidate the market. As 32-bit systems fall off the low end, the new 64-bit software platform will rapidly become entrenched.
::::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id286760}How long will the new 64-bit platform last? {#how-long-will-the-new-64-bit-platform-last .title}

</div>

</div>
:::::

It took 50 years to exhaust the first 32 bits, from the introduction of the Univac through 2005, which roughly matches Moore\'s Law\'s estimate of 48 years. It took 18 years (1987 to 2005) to go from 16 bits to 32 bits. Using the next 32 bits (to exhaust 64 bits) can thus be expected to take anywhere from 36 to 50 years.
::::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id286772}Is 2008 a hard deadline? {#is-2008-a-hard-deadline .title}

</div>

</div>
:::::

The thesis of this paper first occurred to the authors in 2003, when we assembled [an earlier version of the historical memory size table](http://catb.org/esr/halloween/halloween9.html#itanium){target="_top"}. At the time, we doubted our own findings (among other things, suspecting that the switch from desktop to laptop systems would delay the 4 gigabyte wall and introduction of 64-bit hardware). But since then, the rise of x86-64 hardware has occurred right on schedule.

Consider that our trend-curve of address-space growth nailed 2005 as the introduction date for 64-bit systems working from a thirty-year successful retrodiction that includes the [*entire*]{.emphasis} history of the microcomputer back to the Altair^\[[14](world-domination-201.html#ftn.id286797){#id286797}\]^

Consider the fate of OS/2 after the first fully 32-bit version arrived in 1992, two years after Windows 3.0 (and at the same time as Windows 3.1). 1992 also saw the Linux 0.95 release, but even given away for free 32-bit Linux failed to take significant desktop market share away from 32-bit Windows. And remember that Microsoft itself couldn\'t unseat DOS during the 1980\'s with Xenix or early Windows, nor could Digital Research (maker of CP/M) or IBM (with OS/2 1.x).

Yes, 2008 is a [*hard*]{.emphasis} deadline.

More to the point, the obsolescence of 32-bit hardware doesn\'t determine the new software standard, it will merely lock it in place. The decision is happening right now, as each new x86-64 desktop system gets installed. And whatever the new software platform is, history indicates we\'ll be stuck with it for a long time. The forces at work are deep, inexorable --- and predictable.
::::::
:::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.sect1 lang="en"}
::::: titlepage
<div>

<div>

## []{#id286821}Part 2: Which operating system would win the 64-bit desktop today? {#part-2-which-operating-system-would-win-the-64-bit-desktop-today .title style="clear: both"}

</div>

</div>
:::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id286830}The Contenders {#the-contenders .title}

</div>

</div>
:::::

Win64, Linux-64, and MacOS X could all become the standard operating system for 64 bit desktop software. All three have both important strengths and serious problems. This is a look at the current state of each one.
::::::

:::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id286841}Windows x86-64 {#windows-x86-64 .title}

</div>

</div>
:::::

Microsoft long ago shipped 64-bit versions of Windows for Alpha and Itanium, but discontinued them. When it finally shipped x86-64 versions of Windows XP Professional and Server 2003 on April 25, 2005, they didn\'t work very well. Further work on 64-bit Windows was sidelined for a long time by Vista, an enormous undertaking for Microsoft which proved almost beyond the company\'s capabilities, and the company\'s senior management is due to retire in 2008.

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id286853}The Positives {#the-positives .title}

</div>

</div>
:::::

Microsoft [made \$3.5 billion (net) last quarter alone](http://www.microsoftmonitor.com/archives/2006/10/microsoft_fisca_6.html){target="_top"}, and has enough cash on hand to buy a company the size of Home Depot outright. Bill Gates has boasted that Microsoft could run for years without making a dime in revenue, and he\'s right. They have over 70,000 warm bodies to throw at any problem, and a black belt in leveraging their monopoly. Microsoft\'s exclusive distribution contracts with computer resellers still make it difficult to buy a laptop without 32-bit Windows preinstalled, and they\'ve owned not just the current desktop generation but the one before that also.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id286873}The Negatives {#the-negatives .title}

</div>

</div>
:::::

In the first release of this paper, we said \"Vista is still 32-bit\" --- and this was true when we wrote it. Now, in December 2006, there is, in fact, an x86_64 build on the Vista CD-ROM now shipping. But it doesn\'t actually work --- even Microsoft\'s own preferred development tools [don\'t run on it](http://www.eweek.com/article2/0,1895,2072976,00.asp){target="_top"}. It is unclear how much of this is due to problems specific to the 64-bit port versus how much of it is generic to Vista. Nor does that distinction matter much; the point is, the codebase Microsoft is counting on to carry it into the 64-bit world has serious problems.

When, in the fall of 2006, Microsoft finally announced a ship date for Vista after years of repeated delays, it involved the removal of every interesting new feature Vista was originally intended to add to XP. All indications are that Microsoft has fallen back on their old tactic of declaring victory, shipping what they have, and then preparing the first of an endless series of service packs before it even reaches customers.

Underlying these symptoms are serious structural problems. The Windows codebase may now be so huge that it\'s unmaintainable even with heroic effort backed by billions of dollars, and Microsoft\'s business model prevents it from attacking that problem by radically decentralizing development through open source, as Linux and Apple have both done. Today\'s Microsoft is a poster child for the smothering effects of Brooks\' Law.

Even if Microsoft\'s inability to scale the closed-source model proves manageable, Microsoft has undergone a severe brain drain in the past decade. First the antitrust trial hit morale hard circa 1998, then the Vizcaino v. Microsoft lawsuit on the status of their permatemps ^\[[15](world-domination-201.html#ftn.id286910){#id286910}\]^ cost them lots of experienced people. The stock plateaued in 2000, which took away the incentive of anyone there for the money. Now Google is hiring away anyone with a brain who\'s left. ^\[[16](world-domination-201.html#ftn.id286924){#id286924}\]^ There are strong organizational reasons they haven\'t done anything new in six years, it\'s not just bad luck.

Just as importantly, Microsoft is a big established company profiting from the status quo, facing the kind of disruptive change Clayton Christensen described in *The Innovator\'s Dilemma*. Microsoft\'s current customers are not asking for 64-bit operating systems yet, and won\'t until they\'re ready to switch. This is the same situation that left Digital Research and CP/M behind during the 8-bit to 16-bit transition.^\[[17](world-domination-201.html#ftn.id286952){#id286952}\]^

Interestingly, as we were first writing this paper, Bill Gates announced his intention to retire from running Microsoft in 2008 --- the same year we see the 64-bit transition completing. The timing is suggestive, and Gates isn\'t stupid; we assume he can read the hardware trend curves as well as we can. Perhaps, suspecting he knows what\'s coming, he has decided to leave at the top of his game. Gates\' successor, [Ray Ozzie](http://www.wired.com/wired/archive/14.10/microsoft.html){target="_top"}, seems much more open to the idea that there are portions of the universe Microsoft cannot easily consume.

Even more interestingly, in November 2006 Microsoft cut a deal with Novell, the company behind SuSE Linux. The deal included a patent agreement that was cross-licensing in all but name, and an agreement to cooperate on virtualization technology that would allow instances of Windows to run as guests within SuSE Linux.^\[[18](world-domination-201.html#ftn.id286982){#id286982}\]^

We read this as a concession by Microsoft that they have lost the server market to Linux, and they know Vista is not going to reverse that. (Indeed, a [recent IBM survey](http://blogs.zdnet.com/open-source/?p=837){target="_top"} showed 83% of companies expect to support new workloads on Linux in 2007, with only 23% adding new Windows workloads.) Accordingly, Microsoft wants to use the patent threat to attach a per-copy royalty to Linux that can turn into a net revenue generator for them as their server business collapses. But this does not mean Microsoft is conceding the desktop.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287002}The Consequences {#the-consequences .title}

</div>

</div>
:::::

Microsoft doesn\'t get called the Evil Empire for nothing; they know every monopolistic trick for suppressing the competition there is, they are utterly ruthless about using them, and it has already been shown that they can successfully evade anti-trust consequences.

The biggest question about Vista-64 is: will there be one? Can Microsoft overcome its institutional inertia and structural problems to ship something minimally usable before the clock runs out in 2008? If the decision point occurred today, Windows would lose by default.
::::::
::::::::::::::::::

:::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id287020}Mac OS X {#mac-os-x .title}

</div>

</div>
:::::

MacOS X gave the Macintosh an open source BSD based Unix infrastructure, which has had 64-bit versions available for some time, which work pretty well. MacOS X is tied to Apple hardware, which is made entirely from commodity components, now including x86-64 processors.

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287030}The Positives {#the-positives-1 .title}

</div>

</div>
:::::

Steve Jobs brought Apple back from the dead. Mac OS X has third party software support (from *Quicken* to *World of Warcraft*), and handles video and audio just fine (the market lure of iTunes should not be underestimated). It has its act together, is nice and shiny, and has traction now.

OS X is Unix under the hood and its lower levels are open source, giving it many of the same architectural advantages as Linux. Apple has found a way to couple closed and open-source development that lets it put all the DRM, GUIs and multimedia stuff in bits users can\'t reach.

Apple is the fastest growing PC retailer, and its unit volumes are surprising: Apple literally could not manufacture the Mac Mini fast enough. This analysis was conceived when the coauthors discovered we\'d each been independently seriously tempted to buy a Mac Mini, and realized what that temptation implied.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287060}The Negatives {#the-negatives-1 .title}

</div>

</div>
:::::

A major reason OS X can be as slick and hassle-free as it is is that Apple controls the hardware. While Apple is moving closer to PC hardware by switching from Power PC to x86-64, supporting generic PCs would require it to spend huge amounts of money and manpower on compatibility issues it has so far successfully avoided.

Apple\'s current strategy of de-commoditizing PC hardware is a huge stumbling block. Apple\'s current market share seems to be somewhere between [4.8 percent](http://www.macworld.com/news/2006/07/20/marketshare/index.php){target="_top"} and [6.1 percent](http://www.appleinsider.com/article.php?id=2158){target="_top"}. From a sheer infrastructure perspective they\'d have to double production capacity three times over during the next two years to achieve 50% market share.

In addition, Dell, IBM, HP, and hundreds of smaller players aren\'t going away. If Apple won\'t let Dell ship systems that run MacOS X, Dell has no choice but to ship a competitor to MacOS X. No matter how good Apple is, they aren\'t going to become bigger than the entire commodity PC market, which includes white boxes and everything Taiwan can belt out.

Just licensing the Mac hardware design to Dell or other manufacturers won\'t work. If Apple lets clones sell at PC price levels, Apple\'s margins will take a bad hit; if they somehow manage to keep clone prices at Mac-premium levels, what they\'ll have effectively done is just pour more manufacturing capacity into a fixed market share and they\'ll [*still*]{.emphasis} have taken a hit to margins. That\'s unlikely to end well for either Apple or the cloners. ^\[[19](world-domination-201.html#ftn.id287105){#id287105}\]^

Thus, Apple has to know that shooting to replace Windows with OS X in the general desktop market would be a very high-risk proposition. They\'d have to allow it to run on generic hardware --- this means the fat margins from their nice shiny designer hardware would go away at the same time that their OS support costs were exploding.

Another question is, will Jobs be distracted by the content industry? Between Disney, iTunes, Pixar, and iPod, Apple is morphing into a consumer-electronics company married to a music store and a movie studio. It might turn out that Apple never jumps because Steve finds running media companies more interesting.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287130}The Consequences {#the-consequences-1 .title}

</div>

</div>
:::::

If the decision were made today, MacOS X would be essentially unopposed. Nobody else is ready yet. On the other hand, there\'s a real question whether or not Steve Jobs actually wants to win.

Steve Jobs is now the largest stockholder in Disney (and a candidate to become CEO), iTunes and the iPod now drives more of Apple\'s revenue than its computers, and Apple has close cooperative relationships with the RIAA and MPAA. Through Pixar, Jobs became a member of Hollywood\'s inner circle. Driving the Macintosh to victory, and dealing with the aftermath, would take up all his attention for years to come, and he has other things to do with his time. That said, if the market is handed to him on a silver platter, he\'s unlikely to say no.

For the computer industry, the main differences between Apple and Microsoft is that Apple is competent and has good PR. Apple has a history of suing bloggers who leak technical information and developers who tries to clone Aqua\'s look and feel, is the source of closed source binary-only Quicktime and iTunes DRM, and has close cooperative relationships with the RIAA and MPAA.

So far Apple has made all the right defensive moves to avoid losing the 64-bit desktop, but hasn\'t pushed aggressively to win it. If control of the desktop winds up going to Apple by default, Jobs is unlikely to turn it down, but will he pursue it? We don\'t know. Steve Jobs loves keeping his plans secret.
::::::
::::::::::::::::::

:::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id287162}Linux {#linux .title}

</div>

</div>
:::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287166}The Positives {#the-positives-2 .title}

</div>

</div>
:::::

We expect most readers of this paper to be well aware of Linux\'s obvious positives. From Unix, we have the most successful and time-tested OS architecture ever. We have a development community at least an order of magnitude larger than those of all proprietary OS vendors combined. We\'ve had working 64-bit code ports of our OS since 1995. And we have the quality advantages of open-source development, including a level of security and reliability that neither of the other contenders are ever likely to match.

Linux has some less obvious advantages as well. One is that the combination of open source and lots of working driver code makes our driver-migration problem much more tractable than Windows\'s or Mac OS X\'s. In almost all cases, moving a driver to 64 bits is just a recompile.

A victory for Linux would be good for the computer industry because Linux is commodity software. Just as modern PC hardware white boxes consist of interchangeable parts available from multiple vendors, Linux distributions are also created from interchangeable parts available from multiple vendors. Ubuntu, Red Hat, and SuSE are analogous to Dell, Compaq, and Gateway. Only Linux would commoditize the PC software space and create a level playing field no vendor could be shut out of. Both MacOS X and Windows are proprietary and would create a new monopoly, not a standard.

This means that, if the hardware vendors and other people in the computer-industry value chain come to believe Linux has reasonable prospects on the desktop, they [*will*]{.emphasis} jump to it and abandon Microsoft and Apple. All we have to do is look credible. The authors\' informed guess based on previous industry transitions is that 30% desktop market share would be the tipping point.

And Linux is already dominant in the server space.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287209}The Negatives {#the-negatives-2 .title}

</div>

</div>
:::::

Linux is still an operating system developed by geeks and hackers for geeks and hackers. The disconnect between us and the non-technical end user is still vast, and too many of us like it that way and will actually defend our isolation as a virtue.

When somebody with a degree in finance or architecture can grab a Linux laptop and watch episodes of The Daily Show off of Comedy Central\'s website without a bearded Linux geek walking them through an elaborate hand-configuration process first, maybe we\'ll have a prayer.

It\'s also hard to forget that when the call went out for a big company to stand up and fight for DeCSS and open-source 3D drivers, the leading commercial Linux distributor (Red Hat) yanked MP3 playback support from its distro and slunk off into the server market.

Linux on the desktop has been a year or two away for over a decade now, and there are reasons it\'s not there yet. To attract nontechnical end-users, a Linux desktop must work out of the box, ideally preinstalled by the hardware vendor. Right now, Linux is usually an aftermarket upgrade on desktop and laptop systems. Default installations of Linux usually have poor multimedia support, are missing numerous codecs like QuickTime and WMV, and often lack even basic 3D acceleration. Linux can\'t even play DVDs without introducing the risk of lawsuits, and multimedia support files are usually hosted on non-US sites for legal reasons. Third party software support (from *Quicken* to *World of Warcraft*) is almost nonexistent.

You can\'t win the desktop if you don\'t even try. Right now, few in the Linux world are seriously trying. And time is running out.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287252}The Consequences {#the-consequences-2 .title}

</div>

</div>
:::::

Unfortunately \"good\" isn\'t the same as \"ready to happen\". The geeks of the world would like a moonbase too, and it\'s been 30 years without progress on that front. Inevitability doesn\'t guarantee that something will happen within our lifetimes. The 64-bit transition is an opportunity to put Linux on the desktop, but right now it\'s still not ready. If the decision happened today, Linux would remain on the sidelines.
::::::
::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.sect1 lang="en"}
::::: titlepage
<div>

<div>

## []{#id287267}What will it take to win? {#what-will-it-take-to-win .title style="clear: both"}

</div>

</div>
:::::

So what are the requirements for the new 64-bit OS, and what must each of the OS contenders do to meet those requirements? This section will cover the requirements for all three platforms, and examine each individually, but we\'re going to pay special attention to Linux: The \"good news\" and \"bad news\" in each section is for Linux.

The issues we believe to be requirements for the new 64-bit desktop standard platform are, in order of increasing painfulness:

::: itemizedlist
-   Drivers for all major existing hardware.

-   32-bit legacy platform emulation.

-   Surviving the killer app.

-   Enabling preinstalls.

-   Support for all major multimedia formats.
:::

Failure to handle any of these will be a blocking issue to any platform\'s mass adoption by nontechnical end users, without which no platform can hope to achieve the majority market share where network effects make it the new standard.

:::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id287314}Drivers For All Major Existing Hardware {#drivers-for-all-major-existing-hardware .title}

</div>

</div>
:::::

An enormous variety of existing hardware will be attached to x86-64 systems. People who buy a new desktop want to plug in their old PCI cards, attach their old printer, plug in their old DVD burner, use their old scanner, draw with their old tablet\...

New x86-64 motherboards will use many of the same integrated chips for networking, storage, video, and audio, along with controllers for PCI and USB that attach to thousands of devices issued over the last 10 years. Many of the designs for the support chips haven\'t significantly changed in years; they\'re time-tested, fully debugged, available in high volumes, and dirt cheap. Some of the more exotic expansion cards or peripherals aren\'t even being manufactured anymore, but are still in use and would be missed. In sum, a huge dark mass of hardware exists that no brand-new 64 bit OS can support without great effort.

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287333}The Good News {#the-good-news .title}

</div>

</div>
:::::

When it comes to crossing the 32- to 64-bit divide, device driver support is where Linux has its biggest practical advantage over both Microsoft and Apple.

Windows brings to the table a pile of 32 bit binary-only drivers provided to them long ago by vendors. Microsoft doesn\'t have the source code, nor any in-house expertise in this area. They don\'t even have most of the hardware to test against. At best these drivers will run on a 64 bit system under an emulation layer, and if they break Microsoft has no means to update them. Users will get screwed, especially with respect to older hardware no longer supported by a manufacturer.

Just as Windows 3.1 (and even Windows 95) ran for years with 16 bit device drivers dating back to DOS, native 64 bit drivers for Windows-64 will be few and far between for years to come.

MacOS X is intentionally restricted to a limited set of hardware even on 32-bit systems, because Apple can\'t support anything close to the full range of PC hardware either. Tackling generic PC hardware is a step they\'ve explicitly avoided taking, precisely to avoid the hardware support issue.

On the other hand, the Linux community has spent fifteen years expanding our support for PC hardware, and our insistence on open source drivers means that the vast majority of the hardware we support is approximately as well supported on x86-64 as on x86-32. Our platform-specific problems are minor tuning issues, not sealed black boxes that stop working without explanation. Our hardware support isn\'t perfect, but it\'s manageable. For the other two platforms, this issue is their Achilles heel.

Linux\'s established market share in the server market means that failure to provide technical specifications to the Linux community is a career limiting move for a server hardware company. Linux is even in surprisingly good shape supporting laptop hardware, in part due to the rise of blade servers that use laptop components ^\[[20](world-domination-201.html#ftn.id287372){#id287372}\]^.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287407}The Bad News. {#the-bad-news. .title}

</div>

</div>
:::::

Linux\'s weakest area has been 3D acceleration support, simply because Linux servers don\'t need it.^\[[21](world-domination-201.html#ftn.id287414){#id287414}\]^ The [three main players](http://news.zdnet.com/2100-9584_22-6103941.html){target="_top"} in the 3D graphics market are Intel (40% market share), ATI (28%), and Nvidia (20%), and until recently Linux users had to load binary-only modules to get 3D acceleration support on any current 3D graphics chipsets. Luckily, this is no longer the case.

The first modern 3D accelerator family with an open source driver was the ATI Radeon family (supporting Radeon 9600, 9700, 9800, x800, and Mobility M10). Although ATI did not provide an open source driver for these cards, [a reverse engineered driver](http://r300.sourceforge.net){target="_top"} was created, capable of driving the hardware. A reverse engineered driver ignored by the manufacturer cannot be considered \"well supported\", but it was a start.

More recently, Intel decided to be a good guy, releasing as [open source the driver for their newest graphics chipset](http://lists.freedesktop.org/archives/xorg/2006-August/017404.html){target="_top"} before the hardware even shipped. Intel proved it was serious by hiring Keith Packard and Dirk Hohndel to shephard the new driver into X.org and Mesa.^\[[22](world-domination-201.html#ftn.id287456){#id287456}\]^

In this area we still don\'t have complete coverage. Intel\'s graphics chip is only available with Intel processors, not AMD\'s. Although AMD purchased ATI, which may result in the open source drivers from ATI but [hasn\'t yet](http://news.com.com/2061-10791_3-6104655.html){target="_top"}. Still, Linux now explicit support from the largest manufacturer, and has reverse engineered support for the second largest. This leaves Nvidia as the only 3D chipset manufacturer for which Linux users still require binary-only kernel modules, and their market share is only 20%.

We still have problems near wireless hardware as well. Many WiFi vendors refuse to release open-source drivers or even specifications, rationalizing this by claiming (falsely) that US FCC regulations forbid them from shipping radio transmitters with user-controllable power and frequency ^\[[23](world-domination-201.html#ftn.id287481){#id287481}\]^. Most notably, there are no open-source drivers for Intel\'s Centrino wireless hardware. This will probably pass; there is a fully open-source [Centrino driver for OpenBSD](http://kerneltrap.org/node/6650){target="_top"}, and in due course it is likely to be ported.

The Linux community still needs to vote with its dollars, and buy the cards that have the best Linux support. (As with any hardware manufacturer, showing that the existence of an open source driver drives purchasing decisions and translates to increased sales is the only way.) But the situation is no longer dire, merely annoying.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287504}What Linux Needs In Order To Win {#what-linux-needs-in-order-to-win .title}

</div>

</div>
:::::

Luckily, at present our hardware problems are not showstoppers. Two prominent classes of devices are not well supported, but there is hardware in those classes we can deploy, and the vast majority of existing hardware [*is*]{.emphasis} well supported. More open source drivers for the remaining hardware would be nice, but compared to the competition we really are in good shape on the device driver front. At the moment, we can afford to reject binary only kernel modules and still win the 64-bit desktop in 2008.

However, our situation could deteriorate rapidly at any time as each new generation of hardware is introduced. The Centrino mess is a good example of how things can get worse instead of better even when the vendor is a nominal ally that cooperates with the open-source community in other areas.

To prevent similar backsliding from our allies, let alone fend off attacks from outright enemies, we need to shift the aggregate demand that the hardware vendors see. In practice, that means we need a lot of non-technical end users on our side. To avoid the reintroduction of binary-only kernel modules with each new generation of hardware, we must become a large enough market for desktop hardware that hardware vendors need us more than we need them.
::::::
::::::::::::::::::

:::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id287535}Legacy Platform Emulation. {#legacy-platform-emulation. .title}

</div>

</div>
:::::

The huge \"dark matter\" mass of legacy hardware pales in comparison to the black hole of legacy software. Home users have favorite games, utilities, games, macros, games, scripts, games\...^\[[24](world-domination-201.html#ftn.id287543){#id287543}\]^ On the business side, over 80% of all software is written for in-house use, and most of it includes decade-old Windows binaries embodying business logic painfully debugged over many years. Those old apps work, and nobody wants to touch them because it would be expensive and it would break and (often) nobody left at the company understands how to fix them.

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287552}The Good News {#the-good-news-1 .title}

</div>

</div>
:::::

One factor in our favor was the Y2K problem, which forced people to sift through the mass, audit it, and update it. But that was seven years ago, and they only did it to the extent they had to.

Linux runs Windows programs under Wine. This sucked horribly for many years; as the authors once noted ^\[[25](world-domination-201.html#ftn.id287565){#id287565}\]^ the project was in alpha test for almost a full decade. Luckily, Windows more or less stopped being a moving target recently. Our main good news is that Wine has finally caught up enough to have a 0.90 release that sort of worked, followed by a 0.95 release that mostly works, and incremental improvements ever since.

Proprietary forks of the Wine codebase, such as Transgaming\'s Cedega or Codeweavers\' CrossOver Office, have focused on supporting specific niches (games and office software, respectively) of Win-32 software on Linux. They\'ve shown it can be done, and the main Wine codebase is getting closer to a generic solution that\'s fully open sourced.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287587}The Bad News {#the-bad-news .title}

</div>

</div>
:::::

Windows-64 is theoretically at its strongest with backwards compatibility, although this is an issue Microsoft has struggled with in recent years. Joel Spolsky\'s excellent article [How Microsoft Lost the API War](http://www.joelonsoftware.com/articles/APIWar.html){target="_top"} details Microsoft\'s gradual move away from full backwards compatibility, and one of the big complaints about the existing 64-bit Windows release is that it doesn\'t run all the 32-bit Windows programs people have tried on it. How well even 32-bit Vista will run older Windows software is an open question at this point. Microsoft\'s historical practice has been that there is no specification, just a partially documented implementation. When the implementation is the API, changing the implementation can break the API. But since they have the old Windows code, they\'re at least in a position to fix it.^\[[26](world-domination-201.html#ftn.id287607){#id287607}\]^

Apple understands backwards compatibility. The transition to PowerPC processors in the 1990\'s involved bundling an emulation layer into the operating system to run old 68k binaries, and the transition to Intel processors brings with it the \"Rosetta\" emulation layer to run PowerPC binaries. MacOS X also has an emulator that runs a complete installation of MacOS 9, to run old binaries. How MacOS X for Intel will handle running Windows binaries is open to speculation at this point^\[[27](world-domination-201.html#ftn.id287626){#id287626}\]^ but they\'ll probably manage something.

Also, some modern software has a range of [copy prevention technologies](http://www.cdmediaworld.com/hardware/cdrom/cd_protections.shtml){target="_top"}. This does about as much to prevent piracy today as it did back on the Commodore 64 (which is to say effectively nothing), but it presents a headache for emulators that may be accused of breaking DRM just to access the content on a different platform. Transgaming gets around this by licensing some of the more popular DRM formats, so it can support them without getting sued. We\'ll return to this issue later.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287673}What Linux Needs In Order To Win {#what-linux-needs-in-order-to-win-1 .title}

</div>

</div>
:::::

Linux needs a Wine 1.0 release, installed and preconfigured on desktop distributions. The two most important features of Wine 1.0 have to be that (a) it runs legacy Windows-32 binaries correctly, and (b) it does [*not*]{.emphasis} emulate Windows-64, its direct competitor!

If that second \"feature\" seems odd, heed the lesson of OS/2. That operating system bundled a Windows emulator that worked sufficiently well for independent software vendors to ignore native OS/2 support. Vendors wrote for Windows, trusting that the emulator would cover their OS/2 customers.^\[[28](world-domination-201.html#ftn.id287691){#id287691}\]^ As a result, OS/2 was starved of even the Macintosh\'s also-ran level of native application support, and eventually withered on the vine. This is not the fate we want for Linux.

Here is a message for our corporate friends: if you want to help, throw some money and/or developers at Wine. Test your own legacy apps under Wine, send useful bug reports and patches, and follow up. For distributors, preinstall and preconfigure a recent version of Wine, configure Linux to launch it automatically when necessary, and be prepared to support it.^\[[29](world-domination-201.html#ftn.id287732){#id287732}\]^
::::::
::::::::::::::::::

::::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id287747}Surviving The Killer App. {#surviving-the-killer-app. .title}

</div>

</div>
:::::

Past adoptions of new platforms have often been driven by what industry marketing types call a \"killer app\", an application so compelling that many people would buy new hardware and a new operating system to get to it.

Apple II had Visicalc. DOS had Lotus 1-2-3 (a Visicalc clone that could use more than 64K of memory). Early Windows had a version of Solitaire that users were willing to keep Windows around to run. The killer app for the Xbox was the game Halo.

As of yet, there is no killer app for Linux, nor for 64-bit hardware.

To make a strategic difference to Linux during the 32-to-64-bit transition, a killer app would have to have the following set of properties:

::: itemizedlist
-   Not deliverable through a browser (otherwise all contenders will support it about equivalently)

-   Requires 64 bits of address space (otherwise it could be deployed on 32-bit hardware now, and would make no difference to the transition)

-   Can\'t be ported off its home platform, whether for technical or legal reasons.
:::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287790}The Bad News {#the-bad-news-1 .title}

</div>

</div>
:::::

When the open-source world produces compelling applications, they get ported to Windows and the Mac --- obvious examples of this include BitTorrent, OpenOffice, the Firefox web browser, Battle of Wesnoth, etc. Accordingly, Linux cannot really expect to win by hosting a killer app that nobody else can run --- our problem is more in the nature of how to avoid losing market share to a killer app running somewhere else.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287804}The Good News {#the-good-news-2 .title}

</div>

</div>
:::::

As more and more of the services end-users want are delivered through browsers, the space for operating-system-specific killer apps to play in is reduced. LiveJournal and MySpace don\'t care about your underlying OS at all. Google Maps and the Writely word processor may portend a generation of AJAX-using Web applications that offer all the interactivity users actually want.

So the good news is actually the possibility that in a Webbed world the operating-system-specific killer app may be a thing of the past. It would be unwise to count on this, however, so it\'s worth asking what we can do if yet another killer app wades ashore with a case of nuclear halitosis and a yen to destroy Tokyo.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287821}What Linux Needs In Order To Win {#what-linux-needs-in-order-to-win-2 .title}

</div>

</div>
:::::

We can\'t predict what the next killer app might be like, but we can anticipate some things about it simply from the assumption that it can\'t be delivered through a browser or on a 32-bit machine. That suggests our hypothetical monster will be both highly interactive (beyond what Javascript can handle) and memory-hungry. This suggests intensive use of high-bandwith low-latency resources like broadband networking and 3D graphics.^\[[30](world-domination-201.html#ftn.id287832){#id287832}\]^

If that\'s so, most of what we need to do to survive it should reduce to (a) effectively manage huge amounts of RAM in a single-process context, (b) have good 3D graphics support and low latency interactive response, (c) grab market share fast enough that anyone developing a potential killer app also has to deploy it on Linux.
::::::
:::::::::::::::::::

:::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id287860}Enabling Preinstalls {#enabling-preinstalls .title}

</div>

</div>
:::::

The general populace thinks Firefox is an alternative operating system, if they understand the concept at all. It\'s not that they couldn\'t understand the difference between Windows and Linux if they tried, but that\'s what they see, and they actively don\'t want to know anything more. They only notice what\'s underneath when it fails, or when it needs service, or when it costs them money. Waxing eloquent about the implementation, licensing, or development model is like touting the benefits of dual overhead cams with a manual transmission. If grandmother ever has to pop the hood, she has the wrong car.

It\'s not that most people are stupid --- quite the opposite. The smarter people are, the busier they tend to be. Typical doctors, bankers, lawyers, or schoolteachers don\'t care about operating systems because they are smart people who have other things to do. We geeks could change our car\'s oil, fix our own plumbing, do our own taxes, and administer our own systems --- but we\'re busy, we generally just want whatever it is to work and stop distracting us from our programming. Even those of us who are capable of [building our own systems from source code](http://www.linuxfromscratch.org){target="_top"} generally run a prepackaged distribution on our workstations.

Non-technical end users crave the luxury of ignorance. When they buy a new computer, it comes with an operating system, which should work. If they buy a better video card they want the guy at the shop to install it for them, so why should operating systems be any different? Word of mouth is as good as any other way to get people to give Linux a try, but an end-user\'s ideal experience is the iMac\'s three step installation: take it out of the box, plug it in, press the \"on\" button.

To attract enough non-technical end users to make the hardware vendors care about us, we need Linux to come preinstalled on PCs in a configuration that just works. Editing .doc files, viewing DVDs and online video, playing games under Wine, all of it. Getting there is a chicken-and-egg problem; hardware vendors won\'t preinstall unless they see significant demand, which we can only get by having a large userbase, which depends partly on already having preinstalled Linux available.

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id287902}The Bad News {#the-bad-news-2 .title}

</div>

</div>
:::::

We in the open-source community persist in screwing this up. Preinstalled systems come with defaults for everything, even user accounts. Knoppix can boot from CD straight to the desktop. But modern installers still play 20 questions because we can\'t [*imagine*]{.emphasis} them not doing so.^\[[31](world-domination-201.html#ftn.id287914){#id287914}\]^

We also persist in designing in the most obnoxious thing an installer can do, which is to spend several minutes processing or copying files and then ask more questions afterwards. This forces the user to babysit the entire install, which is [*annoying*]{.emphasis}.

But the ease of use of modern installers is a side issue, because even having a perfect installer would not be good enough. Linux needs to come preinstalled and preconfigured, just like the network card and the video card. This means we need to find hardware vendors willing to buck heavy pressure from Microsoft and Apple.

Apple protects its preinstall turf by selling both the hardware and the software; thus the inability to buy a Macintosh without MacOS is unsurprising because it comes as a package deal. All Macintoshes come with MacOS X and A PC vendor who wants to sell computers with MacOS X on them has to sell Macintoshes.

Microsoft doesn\'t sell PCs, but the inability to buy a PC without Windows stopped being surprising many years ago. Microsoft\'s most effective monopolization tactic has always been its exclusive distribution contracts with PC vendors; see [Appendix B, *The Microsoft Tax*](world-domination-201.html#msoft "B. The Microsoft Tax") for a detailed historical analysis of how it has maintained this lock on the market, surviving all competitors, sundry lawsuits and at least two antitrust rulings.

Linux users have attempted to make their voices heard to large OEMs repeatedly over the years, from simply asking to buy Linux preinstalled to elaborate campaigns like [Windows Refund Day](http://www.linuxjournal.com/article/6968){target="_top"}. None of these campaigns have met with any lasting success.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288076}The Good News {#the-good-news-3 .title}

</div>

</div>
:::::

Dell estimates its share of the PC market at 50%, but Dell doesn\'t make its own laptops and laptops outsell desktops. The largest manufacturer of laptops is actually a Taiwanese company called [Quanta Computer](http://www.quantatw.com/e_default.htm){target="_top"}, which manufactures almost 1/3 of the world\'s laptops for other companies to rebadge as Inspirons, Thinkpads, and Powerbooks. Quanta even makes [iPods](http://www.forbes.com/technology/feeds/afx/2006/03/21/afx2611825.html){target="_top"}, yet this company is also the OEM for the Linux-based [One Laptop Per Child](http://www.laptop.org/faq.en_US.html){target="_top"} project.

The fact that most laptops are manufactured overseas by companies even Microsoft can\'t easily intimidate is our main good news on this front. It means smaller vendors can\'t easily be locked out of the laptop market at present. There may be an entrepreneurial opportunity there, if our developers can make Linux interesting to a large enough piece of the consumer market.

Larger vendors are also starting to resist pressure from Microsoft. The recent [waffling by Lenovo](http://news.com.com/Lenovo+denies+ditching+Linux/2100-1003_3-6080115.html){target="_top"}, which now owns IBM\'s Thinkpad line, is a recent example of what looks like pressure from Microsoft being neutralized by a sufficient volume of customer dollars publicly threatening to go elsewhere. But larger vendors only pay attention when they see sales dollars going to someone else.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288126}What Linux Needs In Order To Win {#what-linux-needs-in-order-to-win-3 .title}

</div>

</div>
:::::

The way to get Linux preinstalls starts with this: bypass the vendors Microsoft has under its thumb, and buy from the vendors that specialize in Linux. If only small vendors are willing to do this, they will become large vendors when they get enough sales volume.^\[[32](world-domination-201.html#ftn.id288135){#id288135}\]^ Establish that there [*is*]{.emphasis} a market for preinstalled Linux systems, and that some companies can be successful selling them (not just as a Wal-mart style sideline but as their core business), and larger vendors will take notice.

But voting with our own dollars is only the first step. There simply are not enough current Linux users on the planet to make a mass market. Linux preinstall vendors\' chances of getting enough sales volume depends on our ability to attract non-technical end users. We need millions of Aunt Tillies in our ranks to win. We have to provide a product they want to buy.
::::::
::::::::::::::::::

:::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id288174}The Multimedia Perplex {#the-multimedia-perplex .title}

</div>

</div>
:::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288178}The Bad News {#the-bad-news-3 .title}

</div>

</div>
:::::

Our biggest problem can be summed up in one question: \"What are we going to do about iTunes?\" Apple\'s iTunes is a service that has become lifestyle-critical for tens of millions of people. Try selling Linux to any end-user under 30 and one of the first questions you\'re likely to hear is \"Will it play with my iPod?\"

Some Linux boosters reply that we already know how to enable iPOD users to load songs onto their iPODs, and even how to replace the iPOD firmware with software that doesn\'t have Apple\'s DRM restrictions. This, alas, is just another way of missing the point. It isn\'t what we [*can*]{.emphasis} do that matters, it\'s what we [*can\'t*]{.emphasis} do --- which is supply a legal iTunes client that works out of the box as seamlessly as Apple\'s own software. Technically, this would be easy; it\'s the threat of lawsuits that makes it hard.

But that\'s just the tip of the iceberg, because iTunes isn\'t just audio anymore. According to the [iTunes Video page](http://www.apple.com/itunes/videos){target="_top"}, \"In addition to music videos, the iTunes Music Store also features television shows from ABC, NBC, MTV, ESPN, Sci Fi Channel, Comedy Central, Disney, Nickelodeon and Showtime, among others.\" Nor is iTunes alone. [Warner Brothers is partnering with BitTorrent Inc](http://www.businessweek.com/technology/content/may2006/tc20060508_693082.htm){target="_top"}. [NBC signed a deal with YouTube](http://news.com.com/NBC+strikes+deal+with+YouTube/2100-1025_3-6088617.html){target="_top"}. And don\'t underestimate [Google Video](http://video.google.com/){target="_top"}.^\[[33](world-domination-201.html#ftn.id288237){#id288237}\]^ The internet isn\'t just replacing television someday --- it\'s happening right now.

More generally, there is lots of audio and video content out there in proprietary formats that ordinary computer users want to reach. \"But you should demand it in open-source formats\" is not an answer, it\'s an invitation to be written off as irrelevant.

Serendipitously, the Wall Street Journal\'s Report on Technology made this point as we were first working on this paper. As reporter Mark Golden [wrote](http://online.wsj.com/public/article/SB114727136610348924-Et3a0yO82d_xJdMWN_y8xKXLl7c_20060521.html?mod=blogs){target="_top"} on 15 May 2006: "[Specifically, while the installation and simple functions worked well enough, the systems couldn\'t handle [*all*]{.emphasis} the multimedia applications I needed.]{.quote}" (Emphasis in the original.)

According to Golden, the major blocking issue to Linux\'s desktop growth has changed in the last two years. Golden found our GUIs acceptable enough not to require any mention in the article, and gives the standard productivity applications (word processor, spreadsheet, presentation software) a passing though not perfect grade. It seems clear, even to him, that their remaining problems will be solved in the relatively near term.

Golden emphasizes twice that the real showstopper for Linux adoption by forward-thinking end users is now multimedia capability --- specifically MP3 playback, DVD viewing, AAC and WMA download, and other proprietary codecs. This is perfectly consistent with what the authors of this paper have been hearing from our non-geek friends for two years now, and it should be a wake-up call for our entire community.

OSDL\'s Desktop Linux Working Group has reached similar conclusions by formal market survey. In their [Desktop Linux Client Survey](http://www.osdl.org/dtl/DTL_Survey_Report_Nov2005.pdf){target="_top"} (November 2005), they wrote "[ Ultimately, desktop Linux must provide support for all web content, multimedia or otherwise.]{.quote}" and highlighted formatas including PDF, WMF audio/video, and Quicktime as must-haves.

Just one set of patents, the H.264 patent pool (generally attributed to patents owned by Sorenson), holds up both QuickTime and Flash Video. (In fact [Apple sued Sorensen for licensing its video technology to Macromedia](http://www.oreillynet.com/digitalmedia/blog/2002/05/will_apple_suit_endanger_flash.html){target="_top"}, here\'s [more info on the Sorenson Video Codec v3](http://www.digitalpreservation.gov/formats/fdd/fdd000066.shtml){target="_top"}). There are plenty of open source implementations of this technology (such as [x264](http://developers.videolan.org/x264.html){target="_top"} and [FFmpeg](http://ffmpeg.mplayerhq.hu/legal.html){target="_top"}, but as with DeCSS distributing them raises a sufficient risk of lawsuit that nobody will preinstall them. (Even Ubuntu puts this kind of thing in the \"Universe\" repository, officially unsupported, hosted on overseas servers, and requiring an extra step to enable in the installer. You have to know it\'s there to find it.)
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288336}The Good News {#the-good-news-4 .title}

</div>

</div>
:::::

The best news is that patents eventually expire. For example, the MP3 blocking patent will run out relatively soon, in 2010. But even that will be after the 64-bit transition; MP3 won\'t become unencumbered soon enough to really help us, and many other formats will be legally locked down for much longer.

The other good news is that reverse-engineering isn\'t quite illegal yet, notwithstanding recent abuses of the DMCA. Flash used to be proprietary-only, but after some reverse engineered open-source plugins showed up [Adobe got behind the idea of open sourcing parts of Flash](http://www.adobe.com/aboutadobe/pressroom/pressreleases/200611/110706Mozilla.html){target="_top"} (although this doesn\'t include Flash Video). Sun\'s [release of Java under GPLv2](http://www.sun.com/software/opensource/java/faq.jsp){target="_top"} didn\'t happen in a vacuum either, but in the context of reverse engineered java projects like Apache Tomcat, GNU Classpath, [Harmony](http://lwn.net/Articles/184393/){target="_top"}, and [dozens of others](http://www.gnu.org/software/classpath/stories.html#jvm){target="_top"}. And despite ATI\'s resistance, we already have a reverse engineered open source driver capable of driving most of its 3D chips.

A third piece of good news is that as the transition approaches, third parties are looking beyond Win-32. A year ago the Linux device driver picture was bleak for both 3D and new wireless chipsets, now we have the enthusiastic endorsement of Intel. The open source announcements from Sun and Adobe are welcome news as well, although Apple has positioned itself to benefit from these announcements as much as Linux.

Developing new technology is relatively easy. The [Schrodinger](http://schrodinger.sourceforge.net/){target="_top"} project is a high-quality video codec developed and released in open source by the BBC. Unlike Ogg Theora, there is a huge pile of interesting content backing Scrodinger --- the BBC\'s entire archives. This may be enough of an opening wedge for Schrodinger to spread, but if it were spreading fast enough to make a difference before the end of 2008 we would already be able to see that trend now.

Schrodinger does show that it\'s possible for new open formats to become established, and large chunks of new content to become available in these new formats. There are good open formats out there, but that doesn\'t solve the problem of huge amounts of content being presented today in locked-down formats. If we can\'t even convince National Public Radio to move off of RealAudio in time to make a difference, how are we going to deal with Comedy Central?

These \"good news\" items all have something in common: these problems are eventually solvable, but not in time for the 64-bit transition and the establishment of a new dominant OS. We can do the Right Thing, and eventually we must, but we can\'t always get it done soon enough to matter.

But none of this provides shippable support for DeCSS, the most widely used video codecs, or cleanly integrated MP3 support. The problems with these formats aren\'t technical, but legal. A legal problem generally requires a legal solution, and changing the law requires lots of money and lots of people. We can\'t fix it until we win, but we can\'t win without at least a workaround in place.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288420}What Linux Needs In Order To Win {#what-linux-needs-in-order-to-win-4 .title}

</div>

</div>
:::::

Idealism about open formats will not solve our multimedia problem in time; in fact, getting stuck on either belief in the technical superiority of open source or free-software purism guarantees we will lose. The remaining problems aren\'t technical ones, and none of the interesting patents will expire before the end of 2008.^\[[34](world-domination-201.html#ftn.id288430){#id288430}\]^ We\'ve got to ship something that works now. If we let this be a blocking issue preventing overall Linux adoption during the transition window, we won\'t have the userbase to demand changes in the laws to untangle the screwed up patent system, or even prevent it from getting worse. It\'s a chicken and egg problem, demanding a workaround until a permanent solution can be achieved. We can\'t set the standards until [*after*]{.emphasis} we take over the world.

With a hard deadline approaching fast, it is time to start doing whatever we have to do to get short-term access to proprietary codecs. Commercial Linux distributors, in particular, now face a challenge: solve this problem, or watch the desktop market elude your grasp once again. If that happens, your revenue prospects will be sharply limited by server market.growth.

We\'ll devote the next section of this analysis to examining some plans of attack on the multimedia problem.
::::::
::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::: {.sect1 lang="en"}
::::: titlepage
<div>

<div>

## []{#id288468}Facing The Music {#facing-the-music .title style="clear: both"}

</div>

</div>
:::::

We see six possible approaches to dealing with proprietary codecs. In this section, we\'ll discuss the pros and cons of each and attempt to map a path to victory.

::::::::::::::::::::::::::::::::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id288476}What Are The Alternatives? {#what-are-the-alternatives .title}

</div>

</div>
:::::

::: orderedlist
1.  Do without.

2.  Unload the problem on individual users.

3.  Reverse-engineer all codecs for which deployment is legally possible (e.g. not blocked by patents or the DMCA).

4.  Press for delivery in open formats.

5.  Get closed source binaries that are \"free as in beer\".

6.  Pay to license codecs, per-copy.
:::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288518}Do without. {#do-without. .title}

</div>

</div>
:::::

We can choose to fail. If we don\'t support the media formats that contain the content users want to see, we lose the 64-bit desktop. It\'s that simple. Doing nothing guarantees that we lose, probably to MacOS X.

Every type of content that is unavailable on Linux hands another content-based killer app to a proprietary platform that does support it. Just as we needed a binary-only Netscape in 1998, we\'re going to have to stomach some binary-only crap for now if we hope to be ready in time. If we ignore this issue, the dominant 64-bit platform will be owned by our enemies.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288535}Unload the problem on individual users. {#unload-the-problem-on-individual-users. .title}

</div>

</div>
:::::

Another way of ignoring the problem is to distribute unlicensed copies of Windows codecs^\[[35](world-domination-201.html#ftn.id288542){#id288542}\]^ for use with wrappers like Mplayer\'s.

There are sites outside U.S. jurisdiction that carry packages designed to snap-fit into major Linux distributions and support formats from MP3 to Quicktime. Several multimedia projects (xine, mplayer, and xmms) are designed to accept separately-developed codec plugins, several of the most popular of which are of at best questionable legality in U.S. and many European jurisdictions.

The fundamental problem is that vendors shipping preinstalled Linux won\'t touch this stuff, for obvious reasons. Even distribution-makers won\'t carry these files, or even publicly link to them for fear of contributory infringement lawsuits. Offering them as an aftermarket upgrade is a mitigation strategy at best, and not a good one. The installation procedures for these kind of codecs aren\'t even well-documented, let alone simple enough for nontechnical end-users, and technical support for them is nonexistent.

The gauntlet you have to run to get codec support in this way is so daunting that even the authors of this paper, both among the hardest core of Linux experts, have never been able to keep basic functionality like playing DVDs stable across normal system upgrades.

On top of that, after spending several years carefully distinguishing open-source software from pirated software (despite Microsoft\'s best efforts to conflate the two), depending on end users to laboriously upgrade their machines to receive basic multimedia functionality in a way that leaves them open to potential legal liability is not an appealing strategy.

Some people in our community maintain that this behavior is ethical and the laws against it unjust. We\'re not going to argue for or against that position here; we\'ll just point out that it\'s not a practical solution within our deadline. Instead, it\'s simply a refusal to address the real problem of getting a preinstalled Linux that can handle these formats (without manual upgrades or legal liability) in time to matter.

Nontechnical end-users are not willing to jump through arcane technical hoops. More than that: they expect (and have every right to expect) that a modern operating system will come pre-installed on their hardware and ready to use. Anything that can\'t provide that is just an elaborate way of choosing defeat.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288597}Reverse-engineer codecs {#reverse-engineer-codecs .title}

</div>

</div>
:::::

We\'re good at reverse-engineering. Once Windows versions of a given codec run under Wine, working out what it\'s doing becomes fairly easy.

The problem is that we\'ve already done this for every codec of interest that isn\'t blocked by patents or the DMCA, and even some that are. There is very little ground left to be gained here; the unsupported formats that remain are gated not by technical issues but by patents, by the DMCA\'s anti-circumvention provisions, or [other lawsuits](http://fl1.findlaw.com/news.findlaw.com/hdocs/docs/dvd/dvdccabnnr82503opn.pdf){target="_top"}. And iTunes is a paradigm example; we actually have reverse-engineered open-source support for it, but we can\'t ship it without falling afoul of Apple\'s legal department. A few years ago Linux distributions widely shipped MP3 playback and encoding support, but legal threats have almost eliminated this capability from modern distributions.

Reverse engineered codecs that we can\'t ship without risk of lawsuit are no different than binary-only codecs harvested from Windows that we can\'t ship without lawsuit either. If it doesn\'t give system vendors something they can preinstall, it\'s just not good enough to matter.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288628}Press for delivery in open formats. {#press-for-delivery-in-open-formats. .title}

</div>

</div>
:::::

We\'ve been doing this, and we need to keep doing it. But we can\'t let it become an excuse for ignoring the mountains of content in formats we don\'t support.

The problem with pressing content providers to package in open formats is that we\'re too small a demographic right now. Providing technology isn\'t the problem: Ogg Vorbis and Ogg Theora are wonderful geek projects that have little or no traction in the real world, and Schrodinger is an initiative by one content provider that currently only applies to their own content. Most content providers have no incentive to offer their content in Linux-friendly formats while we remain a tiny minority of desktop users. We\'re statistical noise.

Increasing the amount of content in open formats won\'t eliminate the existence of content in closed formats while we remain a minority platform. At best it will be years before open formats host even a simple majority of available content, let alone everything anyone wants to see.

We can\'t expect major change until providers have reason to fear losing market share unless they ship in open formats. And [*that*]{.emphasis} won\'t happen without tens of millions of end-users demanding it. Which takes us back to the original problem.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288666}Interlude: On Coping With Reality. {#interlude-on-coping-with-reality. .title}

</div>

</div>
:::::

The first four methods of dealing with the proprietary codec issue have two things in common. We\'re already doing them, and they haven\'t solved the problem. It\'s not that they don\'t work, but that we haven\'t got enough time. We need something to ship [*now*]{.emphasis}, because after 2008 the opportunity to capture the desktop during the 64-bit transition will have gone by, and a new incumbent will be in place.

There are a number of format support plugins that we technically have, in open source, but can\'t ship without fear of lawsuit. Examples include DeCSS, reverse engineered iTunes support, MP3 encoding and playback, and FFmpeg. Support for these is not a technical problem, therefore technical solutions do not address the real issues. If hardware vendors preinstall Linux distributions with support for this stuff, selling hardware for-profit, they can expect to get sued. The current legal environment makes these lawsuits inevitable, and we can\'t change the law while remaining a tiny minority.

The largest area suffering from this problem is video codec support. The patented [Sorensen codec in QuickTime](http://apple.slashdot.org/article.pl?sid=02/05/01/2012217){target="_top"} is one problem, the patent pool around [Windows Media Video](http://en.wikipedia.org/wiki/WMV){target="_top"} is another.

So far we have exactly one solution that works today to provide support for video content in proprietary formats: space-shifting binary-only Windows codecs. The [Ubuntu Restricted Formats Page](https://help.ubuntu.com/community/RestrictedFormats){target="_top"} is as close to nontechnical end user support as this approach can come: find a community-supported wiki page by word of mouth, read a legal disclaimer, enable an overseas repository, and install some packages from it at your own risk.

Unfortunately, this does nothing to help hardware vendors seeking to preinstall Linux. Hardware vendors can\'t afford to give away their hardware, and when money changes hands lawsuits have something to go after. Hardware vendors need clear legal title to both the hardware and the software they\'re selling.

The really tough question is: how do we get hardare vendors something they can ship, right now, without having to wait for new legal precedents or changes in the law?
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288730}Secure rights to \"free as in beer\" codecs, possibly with a one-time payment. {#secure-rights-to-free-as-in-beer-codecs-possibly-with-a-one-time-payment. .title}

</div>

</div>
:::::

Some of the codecs we need today are not available under an open source license. We cannot open up these formats (or wean users off of them) without first capturing the user base. This is a classic chicken-and-egg problem.

The problem with space-shifting binary-only Windows codecs isn\'t that it doesn\'t work, it\'s that it\'s not clearly legal. If the community had the legal right to redistribute these codecs (or equivalents), we would have something system vendors could preinstall, long enough to get us over the hump in 2008. (This solution is unpleasant, but no worse than binary-only firmware to support 802.11g wireless cards. And after 2008 we can come up with something better.)

In the best-case scenario, some organization with billions of dollars and community ties could arrange for a CD full of \"free-as-in-beer\" binaries of every codec we need, which could be freely redistributed. Perhaps this would involve a one-time payment for royalties, certification, the development cost of porting an existing binary to Linux, or perhaps just the lawyer time to negotiate and sign cease-fire agreements with the entities who object to DeCSS or MP3 playback, or even licenses to redistribute the existing Windows versions of video codecs for use on Linux via Wine or a wrapper.

This approach might work for codecs which are currently downloadable but not actually a part of Windows. Examples of past success in this area are the Linux ports of the RealAudio and Flash plugins.

Again, the important part is a solution that allows Linux system vendors to preinstall support for these formats. An agreement which allows a codec to be downloaded from a specific website, but which does not allow redistribution of that binary, may not be sufficient to allow system vendors to ship the codec preinstalled on their systems.

As unpleasant as this alternative is, it\'s much more appealing than the final alternative we reluctantly come to.
::::::

:::::: {.sect3 lang="en"}
::::: titlepage
<div>

<div>

#### []{#id288776}Pay royalties to distribute non-free codecs. {#pay-royalties-to-distribute-non-free-codecs. .title}

</div>

</div>
:::::

The previous approaches had one thing in common: they attempt to avoid the conventional proprietary software approach of paying per-copy royalties for software binaries. We\'ve gone to great lengths to avoid facing a simple unfortunate truth: Some IP holders insist on per-copy royalties. If they don\'t get them, they\'re quite prepared to sue. The current legal environment makes it likely they will win if they do.

This reality makes open-source hackers angry and nauseated. But no amount of anger, nausea, or denial will make it go away.

Linux\'s biggest competitors, Apple and Microsoft, are also some of the biggest IP holders in multimedia playback. Apple has already partnered with numerous multimedia content providers, and Microsoft has the dominant platform on which multimedia content providers are trying to deliver their content today. Neither has any incentive to support their proprietary media formats on Linux without a per-copy royalty. Both have repeatedly filed suit to enforce their view of the world, and will do so again.

The member companies of the RIAA and MPAA view the world in much the same way. These groups are made up of content providers, and the normal business practices of content providers includes a royalty stream and an entity prepared to guard their IP rights. They expect everybody else to think the same way, because it\'s what they understand.

We\'ve spent fifteen years educating the world that there is a better way. Now we need to make a fine distinction: per-copy royalties on a driver disk of binary-only userspace multimedia plugins is not the same as a per-copy royalty on Linux itself. The binary-only codecs are a temporary workaround for the problem of how to preinstall a version of Linux that supports all the necessary multimedia formats (without lawsuits bringing the whole enterprise to a grinding halt) long enough to capture the desktop transition ending in 2008.
::::::
:::::::::::::::::::::::::::::::::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id288816}Codecs and the Competitive Minefield {#codecs-and-the-competitive-minefield .title}

</div>

</div>
:::::

It would be a significant challenge to negotiate codec rights even if the only problem were how to offer the IP-holders a royalty rate in the normal range. But before we can get even that far we have to deal with the reality that several of the major codecs are less revenue generators than they are strategic market-control devices.

This is why it may be easier to license redistributable binaries than reach the same agreement for source code. A binary is a known, limited entity. Source code may be modified. Organizations interested in limiting and controlling what people can do are much more comfortable with binaries than with source code.

MP3 and H.264 may be the only major codecs whose controlling entities [*don\'t*]{.emphasis} have obvious interests beyond maximizing their patent royalties. We have existing technology in this area, we just need an agreement allowing us to use it. With the MP3 patent due to expire in 2010, these patent-holders ought to be relatively easy to do deals with.

Unfortunately, nothing after those will be even remotely as easy.

DeCSS represents this problem nicely, because it\'s a market-control device for the MPAA. We have the technology, and probably the legal right to distribute it^\[[36](world-domination-201.html#ftn.id288850){#id288850}\]^ The problem is, the DVDCCA shares a number of traits with SCO. Lawsuits don\'t have to be winnable to be a viable intimidation tactic, especially when the other side has lots of money. We\'ll need lawyers to defend any DeCSS plugin in court, and an organization to stand behind it and defend anyone using it until enough case law piles up establishing that DeCSS isn\'t illegal. In the meantime we\'ll need at least a reliable binary plugin that lets us play DVDs on Linux laptops. Our binary-plugin distributor will either have to be persuasive enough to negotiate a deal with the DVDCCA, or be prepared to withstand a lawsuit (and achieve standing to defend their users from nuisance suits).
::::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id288870}How Not To Do It {#how-not-to-do-it .title}

</div>

</div>
:::::

We need a package of licenses that Linux hardware vendors can use to preinstall multimedia-capable Linux distributions. It\'s possible that each vendor could individually negotiate their own collection of licenses, but that has a big lurking land mine.

The history of Xandros and Lindows/Linspire tells us that the community will reject any attempt to use licensed proprietary codecs as a competitive advantage for any one distribution. This means none of the established distro makers can take this job. It also makes relying on hardware vendors to do it themselves equally problematic, on top of the difficulty and expense of each vendor reinventing the wheel.

We need a sufficient package of multimedia support agreements to be available to all comers on equal terms. This doesn\'t have to be free (in any sense), it could have a royalty payment attached. But it [*must*]{.emphasis} be distribution-agnostic, and vendor-neutral. It also has to exist, which is the tricky part at the moment.

The only way to get such a package of licenses is to have some entity put it together, and stand behind it with money and lawyers. This means a corporation (or arm of a corporate entity) which can sign the appropriate contracts and (alas) pay the appropriate licensing fees. For the sake of discussion, we\'ll call this entity \"Streaming Penguin, Inc.\", and their product \"The Codex\"

The good news is that there are two obvious revenue streams for Streaming Penguin. One is hardware vendors who want to do Linux preinstalls. The other is individual end-users willing to pay a few dollars to buy (or legally download and burn) a CD-ROM full of codecs, put it in the CD-ROM drive on their Linux machine, and press a button to get full legal multimedia support.

This disk of codecs must contain x86-64 versions of all the binary-only plugins necessary to access the content non-technical end users expect to be able to view. The Codex will need .RPM, .DEB, and tarball versions of each component so they can be installed everywhere from Ubuntu to Gentoo, or even hand-installed into Linux From Scratch systems. The codecs must be portable across distributions, userspace-only, and reasonably version-agnostic so that distribution upgrades can usually reinstall the same binaries without the user needing to buy them again.

OEMs will need this CD for Linux preinstalls, and any Linux distributor must be able to resell it directly to individuals. This CD must be equally available to all Linux users, and although it can come bundled with other things users shouldn\'t be required to buy anything else to get it.

Finally, The Codex will probably have to be non-redistributable (if it contains a single non-redistributable codec), and priced so that the revenue from selling it will cover paying royalties back to codec gating entitites demanding licensing fees.

The bad news is that this company is a potential single point of failure for the Linux desktop, and therefore a single point of control.

From day one, Streaming Penguin must be prepared to let the Codex die. It needs to persevere as long as it\'s needed, and then gracefully step down once it has served its purpose. Eventually, if it is successful, Linux will outgrow it as demand shifts to open formats and patents expire. An organization that sees this as a cushy revenue stream will be motivated to preserve the problem, not help the community get past it.
::::::

:::::: {.sect2 lang="en"}
::::: titlepage
<div>

<div>

### []{#id288946}Can Linspire save us? {#can-linspire-save-us .title}

</div>

</div>
:::::

In late July 2006, one of us (Raymond) went public on a panel at at OSCON 2006 with the argument of the previous section. Just minutes later, he was contacted by Kevin Carmony, the CEO of Linux distributor Linspire. Mr. Carmony expressed stong support for our conclusions and a direct interest in addressing the problem.

Linspire, as it turns out, is in a unique position. They are the [*only*]{.emphasis} company with the legal right to ship Linux ports of Windows Media Format codecs, including QuickTime capability. They extracted this concession as part of the settlement of their successful trademark lawsuit against Microsoft.

In August 2006, as a result of having shown a draft of this paper to Kevin Carmony, we were directly involved in the planning for a Linspire product with all the characteristics we have been describing. Linspire wants to be \"Streaming Penguin\" in the hopeful scenario we described above. They even adopted our proposed name for the product: the Codex.

As a result, Eric Raymond joined the Freespire Advisery Board. Freespire is the community development project associated with the Linspire system; its relationship with Linspire is analogous to that between the Fedora project and Red Hat.

Linspire may in fact be able to solve our multimedia problem. They deserve the community\'s support and encouragement for trying.
::::::
:::::::::::::::::::::::::::::::::::::::::::::::::::

::: {.appendix lang="en"}
## []{#history}A. History Of The 8-to-16-to-32-bit Transitions {#a.-history-of-the-8-to-16-to-32-bit-transitions .title style="clear: both"}

The first mover in the 8-bit microcomputer world, Micro Instrumentation and Telemetry Systems (which manufactured the Altair), entered the computer industry (in 1975) in a near-bankrupt state. Because MITS had trouble scaling to meet demand, a restricted supply of Altairs slowed the growth of the nascent PC market until the Altair design was cloned to produce the first commodity hardware platform (CP/M machines based on the S/100 bus).

This delay allowed another company (Apple) to enter the market with a completely different design in 1977, scale production rapidly with venture capital funding, and leapfrog into first place with 50% market share by the time of its one billion dollar IPO in 1980.^\[[37](world-domination-201.html#ftn.id289107){#id289107}\]^

Many smaller players emerged (Commodore, Apple, TI, Tandy) but the number two position was collectively held by the commodity S100 machines running CP/M, and Apple stayed focused on its largest rival before worrying about the smaller targets. This led to a stalemate. The proprietary Apple II hardware couldn\'t take market share away from the commodity S100 hardware, preventing Apple\'s climb up the S-curve to monopoly. But the S100 machines made only glacial headway commoditizing Apple\'s dominant market share. ^\[[38](world-domination-201.html#ftn.id289124){#id289124}\]^

Years later Apple found its market position reversed against IBM\'s PC. Apple\'s Macintosh was a clearly superior product (a 32-bit GUI in a 16-bit command line world), but the PC\'s three-year headstart in the 16-bit space put it beyond 50% market share, and once PC hardware was cloned it gained commodity status as well.^\[[39](world-domination-201.html#ftn.id289135){#id289135}\]^ By uniting commodity hardware with superior market share, the PC swept the field against the Macintosh, Amiga, Atari ST, and others. Later battles after 1990 (Windows vs OS/2, Windows vs. Java, Windows vs Linux) would primarily be fought within the context of PC hardware.^\[[40](world-domination-201.html#ftn.id289143){#id289143}\]^

The current Linux vs Windows battle mirrors the earlier CP/M vs Apple II. Commodity status can be an effective defense against superior market share, but by itself is not an effective offense against it. Linux has survived for 15 years on hardware dominated by Windows, but Linux still cannot be preinstalled on most laptops purchased today.^\[[41](world-domination-201.html#ftn.id289156){#id289156}\]^
:::

::: {.appendix lang="en"}
## []{#msoft}B. The Microsoft Tax {#b.-the-microsoft-tax .title style="clear: both"}

Microsoft\'s entire pricing, contract, and licensing structure is designed with the primary aim of preventing any other operating-system vendor from getting a foothold on the desktop. They achieve this by making the opportunity cost of pre-installing a non-Windows operating system prohibitively high for any vendor who also needs to ship Windows.

The [original 1994 antitrust case against Microsoft](http://www.usdoj.gov/atr/cases/ms_index_licensing.htm){target="_top"} (years before the more recent Microsoft antitrust case of 1998) was over the \"CPU Tax\", which was the nickname for Microsoft\'s per-processor license agreement. By far the cheapest price on DOS an OEM could get was by licensing it per-processor, paying for a copy of DOS for every processor sold. That way the price of DOS was part of the price of the motherboard; as far as end users were concerned DOS was free but any other OS cost them money. What they didn\'t know is it wasn\'t free, it\'s just that even if they used another OS, they still paid for a copy of DOS.^\[[42](world-domination-201.html#ftn.id289209){#id289209}\]^

In theory the CPU tax was ended by the 1994 consent decree^\[[43](world-domination-201.html#ftn.id289230){#id289230}\]^ Microsoft signed to end that lawsuit, but in practice Microsoft weaseled around it by switching to \"per product line\" licensing, requiring OEMs like Dell to set up a separate production line if they wanted to install a non-Windows OS on any of their machines. Microsoft then [lobbied against \"naked PCs\"](http://www.theregister.co.uk/2000/11/28/ms_its_nearly_illegal/){target="_top"}, claiming that shipping systems without any OS preinstalled could not have any purpose but pirating copies of Windows.

Microsoft will literally put an OEM out of business before it lets them help a competitor. This is why big OEMs like Dell keep introducing Linux support and then pulling it again when [Microsoft flexes its muscles](http://www.theregister.co.uk/2002/03/19/microsoft_killed_dell_linux_states/){target="_top"}.

Linux is not the first target of Microsoft\'s vendor lock-in. Back in 1991 Microsoft [used Windows error messages to undermine DR-DOS](http://www.theregister.co.uk/1999/11/05/how_ms_played_the_incompatibility/){target="_top"}. Dirty tricks have been the norm ever since.

In order for IBM to license Windows 95, IBM had to agree not to preinstall OS/2 on any of the PCs it sold (not even the ones that didn\'t have Windows on them). IBM could not ship its own homegrown OS on its own hardware, due to Microsoft\'s monopoly-fueled boycott threat. (In 2005 [Microsoft paid IBM \$850 million](http://www.microsoft.com/presspass/press/2005/jul05/07-01msibmsettlepr.mspx){target="_top"} to settle a lawsuit over this.)

In 1999 BeOS offered its operating system free to any OEM that would preinstall it. When Hitachi took them up on it and offered a machine that would dual boot between Windows and BeOS, Microsoft forced Hitachi to remove all mention of BeOS from the bootloader. So Hitachi shipped a BeOS partition on their machines, but [with no way to boot into it](http://www.kuro5hin.org/story/2001/10/23/13219/110){target="_top"}.

Vendors like Dell have repeatedly introduced, killed, reintroduced, and re-killed support for preinstalled Linux workstations. Michael Dell recently explained [their current public policy](http://www.desktoplinux.com/news/NS3822185143.html){target="_top"}, which boils down to the fact that installing Linux on custom orders of 50 systems or more doesn\'t piss off Microsoft, but offering it as a standard option preinstalled on desktops is something they\'re not allowed to do.^\[[44](world-domination-201.html#ftn.id289350){#id289350}\]^ This isn\'t specific to any one vendor, but is a chronic problem with any large OEM whose business depends on the continuing goodwill of Microsoft. [We just lost Linux preinstalls on the Thinkpad.](http://www.crn.com/sections/infrastructure/infrastructure.jhtml?articleId=188701277){target="_top"}

Antitrust procecution has not broken this pattern, because the laws are hollow and enforcement is toothless. ^\[[45](world-domination-201.html#ftn.id289416){#id289416}\]^

Neither the 1994 consent decree nor the 1998 antitrust conviction have caused any change in Microsoft\'s behavior. The big OEMs do what Microsoft tells them to, and will continue to do so as long as it holds a monopoly. This is another chicken-and-egg problem; only a vendor who can survive without selling any Microsoft products can afford to displease Microsoft.
:::

:::::::::::::::::::::::::::::::::::::::::::::::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[1](world-domination-201.html#id247976){#ftn.id247976}\]^ For a more detailed history of this idea, see Joe Barr\'s [Perceptions of world domination](http://xent.com/pipermail/fork/2002-January/008429.html){target="_top"}.
:::

::: footnote
^\[[2](world-domination-201.html#id248059){#ftn.id248059}\]^ This has already happened twice: the 8-bit microcomputer market crashed in 1984, and the successor to DOS emerged in 1990.
:::

::: footnote
^\[[3](world-domination-201.html#id248804){#ftn.id248804}\]^ Obviously, systems did sell outside this range for other purposes, from embedded systems to mainframes. But that had little or no effect on the desktop market.
:::

::: footnote
^\[[4](world-domination-201.html#id248812){#ftn.id248812}\]^ The doubling time of Moore\'s Law varies by component --- hard drives double slightly faster than average and video resolution doubles more slowly --- but the oft-quoted 18 month figure was derived from Intel\'s original core business, DRAM.
:::

::: footnote
^\[[5](world-domination-201.html#id286509){#ftn.id286509}\]^ With an 18 month doubling time, a few months make a significant difference. The Altair started shipping in April and the PC in August, so these figures are roughly mid-year, but a fudge factor of plus or minus three months is reasonable for regional variations, distribution channel delays, ambient humidity, etc.
:::

::: footnote
^\[[6](world-domination-201.html#id286529){#ftn.id286529}\]^ Most computer hardware and software has enormous up-front development costs, but neglibible incremental (per unit) costs. Thus price is almost entirely a matter of unit volume: the more individual purchases the development costs can be amortized over, the cheaper each individual purchase becomes.
:::

::: footnote
^\[[7](world-domination-201.html#id286551){#ftn.id286551}\]^ The Altair was advertised at the start of 1975 with 256 bytes of memory but was widely considered underpowered, and by mid-year 1K was the standard entry level configuration. The first version of Micro-soft basic needed 7K, but was stripped down to run in 4K because that was considered an unreasonable amount of memory to expect people to buy in 1975. MITS and Micro-soft didn\'t dictate market demand, they adjusted to it.
:::

::: footnote
^\[[8](world-domination-201.html#id286562){#ftn.id286562}\]^ Although we call them 8-bit systems (because their processors had 8-bit registers), both the 8080 and 6502 based systems actually had 16 bits of memory addressing capability (more or less pairing 8-bit registers together to specify an address). Similarly, the 8086 paired together its 16-bit registers to (inefficiently) achieve 20 bit memory addresses. This is why these platforms could address 64 kilobytes and 1 megabyte, respectively. The 386 \"flat memory model\" did away with the need for register pairs, and uses a single 32 bit register to address up to 4 gigabytes of memory. Thus the limit of current 32-bit hardware is actually at 2^32^ bytes, while the 8-bit systems were 2^16^, and the 16-bit systems were 2^20^.
:::

::: footnote
^\[[9](world-domination-201.html#id286586){#ftn.id286586}\]^ The Altair\'s successors ran an 8-bit operating system called CP/M, but memory was so scarce that loading an OS from disk wasn\'t popular in the 8-bit world.
:::

::: footnote
^\[[10](world-domination-201.html#id286603){#ftn.id286603}\]^ The famous \"640k barrier\" was the result of some unfortunate programming decisions in DOS, placing I/O memory at an even 10 times the old 64k limit and thus making it unavailable to programs. This could be worked around with tricks like \"LOADHI\", and by moving start of video memory, but only up to the 1 megabyte addressing range of the processor.
:::

::: footnote
^\[[11](world-domination-201.html#id286630){#ftn.id286630}\]^ The sudden success of Windows 3.0 came as a surprise to Microsoft. The 1M memory barrier was broken by a programmer named David Weise, who invented thunking and gave existing 16-bit Windows programs the ability to use 4G of memory without even needing to be recompiled. Breaking the 640K barrier in Windows 3.0 wasn\'t a Microsoft corporate initiative, it was [one guy who did the impossible and changed history](http://blogs.msdn.com/larryosterman/archive/2005/02/02/365635.aspx){target="_top"}. The only interesting thing Windows 3.0 could do was allow its programs use more than 1M of memory, but at the time that was the most important thing it could possibly do. Although IBM shipped OS/2 2.0 two years later (31 March 1992, a few days before Windows 3.1\'s 6 April 1992 release), it was just too late. Windows had already picked up enough users from the previous pathetic but timely version to become the new standard.
:::

::: footnote
^\[[12](world-domination-201.html#id286682){#ftn.id286682}\]^ It could have been PowerPC, perhaps if the Cell processor had been ready by christmas of 2004. But it\'s too late now. Even Apple has switched from Power PC to x86-64, in part to take advantage of the economies of scale from the new standard PC platform. 64-bit Laptops have been available for a year now from [the largest vendors](http://arstechnica.com/news.ars/post/20050623-5030.html){target="_top"} to [the smallest](http://www.linuxcertified.com/linux-laptop-lc2464.html){target="_top"}, and AMD already has a new generation of its 64-bit processor design (Turion) focused on low power consumption.

A significant factor in the decision was power consumption. Ever since [notebook sales passed desktop volume](http://news.com.com/PC+milestone--notebooks+outsell+desktops/2100-1047_3-5731417.html){target="_top"} in May 2005, the power-to-performance ratio has been about as important as price-to-performance. Since no other 64-bit platform offered a laptop option, x86-64 won that niche by default.
:::

::: footnote
^\[[13](world-domination-201.html#id286722){#ftn.id286722}\]^ Every platform grows memory extensions as it nears its end of life. The 8-bit systems had a technique called \"bank switching\", the DOS machines limped along with extended/expanded/extruded memory, and these days we have Intel\'s Page Addressing Extensions. It doesn\'t matter; rewriting software to jump through these hoops is about as much work as porting the software to a new platform where accessing more memory is natural.
:::

::: footnote
^\[[14](world-domination-201.html#id286797){#ftn.id286797}\]^ In retrospect, one of the many reasons for the abject failure of Intel\'s 64-bit Itanium processor was that 1998 was just too early.
:::

::: footnote
^\[[15](world-domination-201.html#id286910){#ftn.id286910}\]^ \"Permatemps\" are \"permanent temporaries\". A dodge to hire people at below-market rates turned into a divisive labor dispute and then a legal nightmare. You can find pointers to the history of the lawsuit [here](http://en.wikipedia.org/wiki/Permatemp){target="_top"}.
:::

::: footnote
^\[[16](world-domination-201.html#id286924){#ftn.id286924}\]^ Anyone interested in following internal goings-on in Redmond, try reading the [Mini-Microsoft](http://minimsft.blogspot.com){target="_top"} blog and this Business Week [article](http://www.businessweek.com/magazine/content/05_39/b3952009.htm){target="_top"} about it.
:::

::: footnote
^\[[17](world-domination-201.html#id286952){#ftn.id286952}\]^ Back in the 8-bit world Digital Research owned the dominant disk-based OS, CP/M. (Systems that didn\'t have BASIC burned into ROM generally ran it under CP/M.) Microsoft\'s DOS began as a clone of CP/M-86 (the 16-bit version of CP/M) which was then extended with Unix features. During the transition Digital Research stayed focused on the existing 8-bit market, where it was making all its money, leaving Microsoft virtually unchallenged in the 16-bit PC market for the first few years. When the 8-bit market finally collapsed in 1984, Microsoft and DOS were already entrenched. The remains of Digital Research were purchased by Novell a few years later.
:::

::: footnote
^\[[18](world-domination-201.html#id286982){#ftn.id286982}\]^ The sight of Steve Ballmer on video talking about how important Linux is to Microsoft customers was priceless.
:::

::: footnote
^\[[19](world-domination-201.html#id287105){#ftn.id287105}\]^ And that\'s without taking into account what happened to [the last company](http://www.businessweek.com/1997/35/b3542086.htm){target="_top"} that Apple allowed to sell Mac clones.
:::

::: footnote
^\[[20](world-domination-201.html#id287372){#ftn.id287372}\]^ Notebooks now sell in greater dollar volume and greater unit volume than desktop systems, thus the economies of scale have switched over to laptop components. Since computer manufacturing is dominated by start up costs with much lower incremental costs, pricing of computer components is almost entirely a matter of unit volume. This means that laptop components are getting cheap fast, and although desktop components had a head start amortizing their start-up costs, laptops have all the new R&D budget and are already pulling ahead on the price to performance ratio, a gap which will only grow wider.

The other important metric is the power to performance ratio, where laptops already had an advantage because of battery life issues and because the components operate in a confined space where heat dissipation is a problem and the noise from a fan is in the user\'s face rather than under a desk. Heat dissipation is also a major limiting factor in server cluster density, where power consumption is directly correlated to heat to be dissipated. On top of that, energy costs are often the dominant cost factor running a server cluster long-term, both to run the cluster and to cool it.

All this together means that laptop components have been widely used in the server space for several years now, so Linux runs well here. The UPS monitors morphed into laptop battery monitors years ago, and the pioneering seamless hardware autodetection work done by Red Hat kudzu and Knoppix has been adopted by other distributions. We\'re in good shape here.
:::

::: footnote
^\[[21](world-domination-201.html#id287414){#ftn.id287414}\]^ Even wireless access needs a server for your laptop to talk to, and that server often runs Linux. It wasn\'t smooth or easy getting those drivers open-sourced, but there was a strong business case from the point of view of the hardware manufacturers for having that hardware not just supported on Linux but well supported, and the embedded portion of the market demanded cross-platform support for low-power ARM and MIPS processors. This drove enough purchasing decisions to matter, and the vendors followed the money, as always.
:::

::: footnote
^\[[22](world-domination-201.html#id287456){#ftn.id287456}\]^ Interestingly, Intel is on the fence about the 64-bit transition. They\'ve partnered with Apple and are playing nice with Linux. Whatever the new operating system standard is, they\'ve positioned themselves to survive and prosper from it.
:::

::: footnote
^\[[23](world-domination-201.html#id287481){#ftn.id287481}\]^ In fact, the FCC regulations governing transmitter power are binding on the transmitter operators, not on equipment manufacturers. What the WiFi manufacturers are actually doing is using the FCC as an excuse to hide driver logic they don\'t want competitors to see, especially in the area of power-management algorithms.
:::

::: footnote
^\[[24](world-domination-201.html#id287543){#ftn.id287543}\]^ Did I mention games?
:::

::: footnote
^\[[25](world-domination-201.html#id287565){#ftn.id287565}\]^ See [DRAG.NET: A Windows-to-Linux Migration Case Study and Vaudeville Routine](../dragnet/dragnet.html){target="_top"}, which seemed funny at the time.
:::

::: footnote
^\[[26](world-domination-201.html#id287607){#ftn.id287607}\]^ The problem with having a million monkeys at a million typewriters is that it leaves a heck of an editorial cleanup job. Microsoft seems to have assumed that since its competitors [found a way around Brooks\' Law](http://www-128.ibm.com/developerworks/linux/library/os-merrier.html){target="_top"}, it was also immune. This might be why Vista took so long.
:::

::: footnote
^\[[27](world-domination-201.html#id287626){#ftn.id287626}\]^ Computer historian Robert X. Cringely of PBS speculated extensively about Apple\'s strategy to support Windows in four consecutive columns ([one](http://www.pbs.org/cringely/pulpit/pulpit20060406.html){target="_top"}, [two](http://www.pbs.org/cringely/pulpit/pulpit20060413.html){target="_top"}, [three](http://www.pbs.org/cringely/pulpit/pulpit20060420.html){target="_top"}, and [four](http://www.pbs.org/cringely/pulpit/pulpit20060427.html){target="_top"}), but as usual Steve Jobs is keeping his plans secret until he\'s ready to implement them.
:::

::: footnote
^\[[28](world-domination-201.html#id287691){#ftn.id287691}\]^ As usual, the real world is more complicated than we can cleanly cover in a paper of finite length. We\'ve already mentioned that OS/2 2.0 shipped a year after Windows 3.0, but that wasn\'t the end of the story. After Windows 3.1 shipped, Microsoft pulled a nasty trick by forcing vendors who wanted access to betas of the next version of Windows (which eventually became Windows 95) to sign a non-disclosure agreement that forbid them from shipping new versions of their software for non-Windows platforms before the new Windows shipped. Vendors signed up because they needed something to develop the next generation of software against, and Microsoft\'s excuse was that vendors might take design ideas from the new Windows and implement them on other operating systems before shipping them for Windows. In reality, this meant that when the Windows 4.0/Chicago/Windows 95 ship schedule slipped by around three years (practice for the current Blackcomb/Longhorn/Vista slip), vendors were left with nothing to ship. Several software vendors went bankrupt waiting, some of which Microsoft bought cheaply. (To stave off a full-scale revolt, Microsoft eventually even introduced a service pack, Win32-s, which retrofit a subset of the new Windows\' API onto Windows 3.1 to let software vendors ship their new Windows programs for the old operating system.)

The point of this exposition about OS/2 is that Microsoft pulled a lot of dirty tricks to turn small mistakes on IBM\'s part into big ones. We\'re up against smart people with lots of money, and there\'s no magic bullet guaranteeing success. We have to do lots of right things and avoid lots of wrong things.
:::

::: footnote
^\[[29](world-domination-201.html#id287732){#ftn.id287732}\]^ If we seem to be harping on World of Warcraft, remember that this one game has over 7 million paying subscribers and is now generating [one billion dollars per year](http://www.mania.com/52187.html){target="_top"} for its parent company, Blizzard. That\'s an entire industry of its own, and is exactly the sort of thing that needs to work out of the box on Linux to attract non-technical end users.
:::

::: footnote
^\[[30](world-domination-201.html#id287832){#ftn.id287832}\]^ Traditionally games have pushed the hardware in the desktop space, and motivated early hardware adopters. We note that A 64-bit successor to [World of Warcraft](http://www.worldofwarcraft.com){target="_top"} could have the properties described, yet be acceptable to most Linux users as a proprietary program they might be willing to install. Games avoid one of the of the main objections to proprietary software is the question of ownership. If I create a document using a proprietary word processor, the owner of the word processor can control my access to my document. Using a tool to create a product does not mean the owner of the tool then owns the product, but if the tool is still needed to use the product ownership is compromised. Any application that can control my access to my own work can potentially exert control over and thereby claim an ownership stake to my own work. If my OS vendor can shut off my operating system for nonpayment, they can hold my data hostage, even though I created that data and it clearly should not belong to them. This tension is generally not present with games, which either don\'t create valuable derived works or do so in the context of a subscription service where the ownership issues are clearly spelled out up front.
:::

::: footnote
^\[[31](world-domination-201.html#id287914){#ftn.id287914}\]^ The only question they should probably ask by default is "[Hi, I\'m about to wipe your system and put Linux on it, that ok?]{.quote}" Have an \"Expert\" button for OEMs, recognizing that most geeks act as their own OEM. Maybe prompt them for user account information on the first boot, but have a \"guest\" account that just works. Don\'t force time-zone setting at installation time; instead, allow the users to set it later by clicking the clock on the desktop when they get around to it.
:::

::: footnote
^\[[32](world-domination-201.html#id288135){#ftn.id288135}\]^ A quick Google found [LinuxCertified](http://www.linuxcertified.com/linux_laptops.html){target="_top"}, [SWT](http://www.swt.com/notebooks.html){target="_top"}, and [Emperor Linux](http://www.emperorlinux.com/){target="_top"}. This is not an endorsement of any specific vendors, and there are bound to be others.
:::

::: footnote
^\[[33](world-domination-201.html#id288237){#ftn.id288237}\]^ We wrote that bit before Google bought YouTube. It\'s impossible to keep up.
:::

::: footnote
^\[[34](world-domination-201.html#id288430){#ftn.id288430}\]^ Just determining what the applicable patents are can be nontrivial. If somebody could tell us what the actual Sorenson patents at issue are, and when they expire, we\'d appreciate it. This [press release](http://www.mpegla.com/news/n_03-11-17_avc.html){target="_top"} is the closest we\'ve come, which says they run through at least the end of 2010.
:::

::: footnote
^\[[35](world-domination-201.html#id288542){#ftn.id288542}\]^ The legal theory behind many of these codecs is that if you have a copy of Windows installed on a machine, then copying these codecs from your Windows partition to your Linux partition is perfectly legal space shifting. Unfortunately, harvesting the codec files off a random Windows filesystem is a tricky problem, and the results tend to be extremely flaky due to things like version skew. (And this is assuming you didn\'t blow away Windows to install Linux, or that you even had a Windows partition on the machine in the first place.) It\'s much easier to ship a known set of codecs that have been properly wrapped and tested. The downside is it\'s somebody else\'s copyrighted binaries, with no license to redistribute them.
:::

::: footnote
^\[[36](world-domination-201.html#id288850){#ftn.id288850}\]^ DeCSS isn\'t a trade secret anymore thanks to Hoy Exhibit B, where the DVDCCA itself submitted the DeCSS source code unsealed, letting a clearly unconstrained copy out into to the world. See [the EFF\'s page on the DVDCCA cases](http://www.eff.org/IP/Video/DVDCCA_case/){target="_top"} for details.
:::

::: footnote
^\[[37](world-domination-201.html#id289107){#ftn.id289107}\]^ As new players emerged, those designed based on the same processor as the Altair (the Intel 8080) tended to evolve into CP/M clones, while the designs based on other processors (such as the MOS 6502 used in the Apple II) usually used a ROM BASIC operating system. ROM-based operating systems meant the 8-bit world had a hard time consolidating because there was no such thing as a reinstall; switching operating systems involved throwing the old hardware away. ROM BASIC provided a similar kind of \"source but not binary compatability, and you have to tweak the source\" found in the proprietary Unix market a few years later. History repeats itself all over the place.
:::

::: footnote
^\[[38](world-domination-201.html#id289124){#ftn.id289124}\]^ The Apple II actually outlived CP/M. The Apple IIc Plus was released in September 1988, after Digital Research had lost a lawsuit with apple over the GEM GUI, and retooled CP/M into the DOS clone DR-DOS.
:::

::: footnote
^\[[39](world-domination-201.html#id289135){#ftn.id289135}\]^ PC hardware was unusually vulnerable to cloning because it was designed as a 16-bit successor to Apple\'s largest competitor, the commodity CP/M machines.
:::

::: footnote
^\[[40](world-domination-201.html#id289143){#ftn.id289143}\]^ Even though the 1984 Macintosh GUI wasn\'t fully cloned in the PC world for 11 years (with Windows 95 moving the Apple menu to the bottom of the screen and renaming it \"Start\"), the Macintosh was gradually reduced to near-irrelevance during that period. The revival of the Macintosh since Steve Jobs\' return is a recent phenomenon, and of the many intelligent plays (iMac, Mac OS X, iPod, iTunes) Jobs has made since returning as Apple\'s CEO, the most recent is rebasing the Macintosh onto commodity PC hardware.
:::

::: footnote
^\[[41](world-domination-201.html#id289156){#ftn.id289156}\]^ Indeed, in some important ways Linux would have more difficulty displacing a dominant 64-bit OS than the historical record suggests. The idea of a commodity market for computers is no longer new, surprising, or dismissably radical. A dominant proprietary vendor that recognizes a threat can respond with more formidable defenses than CP/M faced and failed to overcome. A monopolist\'s virtually unlimited budget can afford to come up with a new roadblock to throw in a competitor\'s path every few years to maintain the status quo. Linux has already faced a stream of obstacles in the 32-bit world; winmodems, IE-only websites, the SCO lawsuit, laws like the DMCA, the prospect of hardware DRM, exclusive contracts with the largest system vendors, closed-source drivers for critical hardware (currently graphics and wireless), and more. These moves cannot destroy Linux, but they\'ve done a good job of bottling it up in its niche, and they suck up its development cycles with endless distractions. Replacing Microsoft with Apple wouldn\'t help matters much, because they\'re just as intensely proprietary and on top of that, they\'re not fundamentally incompetent at this whole \"computer\" thing.
:::

:::: footnote
^\[[42](world-domination-201.html#id289209){#ftn.id289209}\]^ The 1994 antitrust case began with the [complaint](http://www.usdoj.gov/atr/cases/f0000/0046.htm){target="_top"}:

::: blockquote
> Virtually all major PC manufacturers find it necessary to offer Microsoft operating systems on most of their PCs. Microsoft\'s monopoly power allows it to induce these manufacturers to enter into anticompetitive, long-term licenses under which they must pay royalties to Microsoft not only when they sell PCs containing Microsoft\'s operating systems, but also when they sell PCs containing non-Microsoft operating systems.
:::
::::

:::: footnote
^\[[43](world-domination-201.html#id289230){#ftn.id289230}\]^ The 1994 action resulted in a [consent decree](http://www.usdoj.gov/atr/cases/f0000/0047.htm){target="_top"} saying, among other things:

::: blockquote
> ::: itemizedlist
> -   \(B\) Microsoft shall not enter into any License Agreement that by its terms prohibits or restricts the OEM\'s licensing, sale or distribution of any non-Microsoft Operating System Software product.
>
> -   \(C\) Microsoft shall not enter into any Per Processor License.
> :::
:::

The consent decree went on to list a bunch of other things Microsoft was doing at the time, such as bundling products to leverage its OS monopoly to take over the office software market, all of which Microsoft theoretically promised to stop doing, but went on doing anyway. Microsoft also seems to have signed, then appealed the consent decree. (Don\'t ask\....)

For a more recent list of the dirty tricks Microsoft pulls to maintain its monopoly on vendor preinstalls, read the [findings of fact](http://www.usdoj.gov/atr/cases/f3800/msjudgex.htm){target="_top"} from the 1998 antitrust trail, which was just as completely ineffective as the 1994 action.
::::

::: footnote
^\[[44](world-domination-201.html#id289350){#ftn.id289350}\]^ Here are various references to Dell\'s changing stances about Linux, from [1999](http://news.com.com/Dell+hops+on+Linux+locomotive/2100-1001_3-223304.html){target="_top"}, [2000](http://www.techweb.com/wire/story/TWB20000815S0014){target="_top"}, [2001](http://www.newsforge.com/article.pl?sid=01/11/19/2242229){target="_top"}, [2002](http://www.theregister.co.uk/2002/03/19/microsoft_killed_dell_linux_states/){target="_top"}, [2003](http://www.dell.com/downloads/global/corporate/iar/20030701_dhb.pdf){target="_top"}, [2004](http://www.theregister.co.uk/2004/07/07/dell_vs_questar/){target="_top"}, [2005](http://www.theregister.co.uk/2005/10/06/dell_open_pc/){target="_top"}, and [2006](http://www.eweek.com/article2/0,1895,1930851,00.asp){target="_top"}.
:::

::: footnote
^\[[45](world-domination-201.html#id289416){#ftn.id289416}\]^ Some people think the toothlessness of antitrust law is a contingent feature of today\'s political environment, but both history and the discipline of [public-choice theory](http://en.wikipedia.org/wiki/Public_choice_theory){target="_top"} teach us that co-opted regulators favoring the politically connected is actually the expected and normal situation.
:::
::::::::::::::::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
