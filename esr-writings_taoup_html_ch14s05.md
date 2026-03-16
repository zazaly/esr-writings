::: navheader
  Trends for the Future                                          
  -------------------------------------- ----------------------- --------------------------------------
  [Prev](ch14s04.html){accesskey="p"}     Chapter 14. Languages     [Next](ch14s06.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2978170}Trends for the Future {#trends-for-the-future .title style="clear: both"}

</div>
::::

[Table 14.1](ch14s05.html#lang_usage "Table 14.1. Language choices.") gives a rough indication of today\'s distribution of language usage. We give figures from both SourceForge^\[[128](ch14s05.html#ftn.id2978184){#id2978184}\]^ and Freshmeat,^\[[129](ch14s05.html#ftn.id2978197){#id2978197}\]^ the two most important new-release sites, as of March 2003.

The SourceForge figures are soft in several ways: Notably, SourceForge\'s query interface doesn\'t permit filtering on OS and language simultaneously, so some of these numbers represent MacOS and Windows projects. The effect is probably to exaggerate C++[]{#id2978219 .indexterm} and Java\'s[]{#id2978227 .indexterm} share considerably. However, Unix-based projects dominate sufficiently (by about a 3:1 ratio) so that the effect on the figures for languages other than these is probably not too distorting.

The Freshmeat sample is smaller, but the site hosts only Unix-based releases --- and it counts actual releases, not the huge clutter of failed and inactive SourceForge projects. It is thus interesting that the population figures track SourceForge\'s by about a 1:2 ratio except in precisely the cases (C++ and Java) where we would expect them to be out of proportion because of the absence of Windows projects.

::: table
[]{#lang_usage}

**Table 14.1. Language choices.**

  Language     SourceForge   Freshmeat
  ------------ ------------- -----------
  C            10296         4845
  C++          9880          2098
  Shell        1058          487
  Perl         4394          2508
  Tcl          649           328
  Python       2222          948
  Java         8032          1900
  Emacs Lisp   ?             31
:::

This chapter was first drafted in 1997; at time of writing it is mid-2003. That is a long enough time base that the relative positions of the languages we surveyed above have changed somewhat since first writing, indicating adoption trends that may suggest what their futures will be like. (Community size is an important predictor of the quality and amount of work that will go into improving the most-used open-source implementations of these languages; both growth and decline tend to be self-reinforcing.)

Broadly speaking, C[]{#id2978443 .indexterm} and C++[]{#id2978455 .indexterm} and Emacs Lisp[]{#id2978464 .indexterm} have remained stable across the 1997-2003 time period, appealing to much the same constituencies in 2003 as they did in 1997. C has gained slowly at the expense of older conventional languages such as FORTRAN; C++, on the other hand, has lost some ground to Java[]{#id2978477 .indexterm}.

Perl[]{#id2978490 .indexterm} usage has grown respectably, but the language itself has been stagnant for some time. Perl\'s internals are notoriously grubby; it\'s been understood for years that the language\'s implementation needs to be rewritten from scratch, but an attempt in 1999 failed and another seems presently stalled in mid-2003. Nevertheless, Perl is still the 800-pound gorilla of scripting languages[]{#id2978505 .indexterm}, and dominates Web scripting and CGI.

Tcl[]{#id2978518 .indexterm} has been in a period of relative decline, or at least of diminishing visibility. In 1996 a widely-reported and plausible estimate of community sizes held that for every Python[]{#id2978530 .indexterm} hacker there were five Tcl[]{#id2978539 .indexterm} hackers and twelve Perl[]{#id2978548 .indexterm} hackers. Today the SourceForge figures suggest those ratios are about 3:1:7. However, Tcl is reported to be very widely used for scripting of specialized components in several industries, including electronic design automation, radio and television broadcasting, and the film industry.

Python[]{#id2978566 .indexterm} has risen in popularity as rapidly as Tcl[]{#id2978575 .indexterm} has fallen. Though the Perl[]{#id2978584 .indexterm} community is still twice the size of Python\'s, a visible tendency of the brightest Perl hackers to migrate to Python has been rather ominous for the former language --- especially as there is no migration at all in the opposite direction.

Java[]{#id2978601 .indexterm} has become widely used at sites already invested in Sun Microsystems[]{#id2978610 .indexterm} technology and is in increasing deployment as an instructional language in undergraduate computer science curricula. Elsewhere, however, it is only marginally more popular than it was in 1997. Sun\'s determination to stick to a proprietary licensing model has prevented the major breakout many observers then predicted; under Linux[]{#id2978625 .indexterm} and in the wider open-source community Java has not made the headway against C that it has elsewhere.

No new general-purpose language has emerged to seriously challenge those we\'ve surveyed here. PHP is making inroads in Web development, challenging Perl CGIs (as well as ASP and server-side Java[]{#id2978643 .indexterm}) but is almost never used for standalone programming. Non-Emacs Lisp[]{#id2978653 .indexterm} dialects, a once-promising area that seemed headed for a renaissance in the mid-1990s, have continued to fade. Recent efforts such as Ruby (a sort of Python-Perl-Smalltalk cross developed in Japan) and Squeak (an open-source Smalltalk port) look promising, but have so far neither attracted hackers far outside their development groups nor demonstrated staying power.

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[128](ch14s05.html#id2978184){#ftn.id2978184}\]^ [Query for statistics](http://sourceforge.net/softwaremap/trove_list.php?form_cat=160){target="_top"}.
:::

::: footnote
^\[[129](ch14s05.html#id2978197){#ftn.id2978197}\]^ [Query for statistics](http://freshmeat.net/browse/160/?topic_id=160){target="_top"}.
:::
:::::
:::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- -------------------------------------------- --------------------------------------
  [Prev](ch14s04.html){accesskey="p"}     [Up](languageschapter.html){accesskey="u"}     [Next](ch14s06.html){accesskey="n"}
  Language Evaluations                        [Home](index.html){accesskey="h"}                        Choosing an X Toolkit
  -------------------------------------- -------------------------------------------- --------------------------------------
:::
