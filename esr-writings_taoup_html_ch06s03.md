::: navheader
  Designing for Maintainability                                    
  -------------------------------------- ------------------------- --------------------------------------------------
  [Prev](ch06s02.html){accesskey="p"}     Chapter 6. Transparency     [Next](multiprogramchapter.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2915209}Designing for Maintainability {#designing-for-maintainability .title style="clear: both"}

</div>
::::

Software is maintainable to the extent that people who are not its author can successfully understand and modify it. Maintainability demands more than code that works; it demands code that follows the Rule of Clarity and communicates successfully to human beings as well as the computer.

Unix programmers have a lot of implicit knowledge available to them about what makes for maintainable code, because Unix hosts source code that goes back decades. For reasons we\'ll discuss in [Chapter 17](http://www.catb.org/~esr/writings/taoup/html/portabilitychapter.html "Chapter 17. Portability"), Unix programmers learn a tendency to scrap and rebuild rather than patching grubby code (see Rob Pike\'s meditation on this subject in [Chapter 1](philosophychapter.html "Chapter 1. Philosophy")). Thus, any sources that have survived more than a decade of evolutionary pressure have been selected for maintainability. These old, successful, well-established projects with maintainable code are the community\'s models for practice.

A question Unix programmers --- and especially Unix programmers in the open-source world --- learn to ask about tools they are evaluating for use is: "Is this code live, dormant, or dead?" Live code has an active developer community attached to it. Dormant code has often become dormant because the pain of maintaining it exceeded its utility to its originators. Dead code has been dormant for so long that it would be easier to reimplement an equivalent from scratch. If you want your code to live, investing effort to make it maintainable (and therefore attractive to future maintainers) will be one of the most effective ways you can spend your time.

Code that is designed to be both transparent and discoverable[]{#id2915277 .indexterm} has gone a long way toward being maintainable. But there are other practices we can observe in the model projects in this chapter that are worth emulating.

One very important practice is an application of the Rule of Clarity: choosing simple algorithms. In [Chapter 1](philosophychapter.html "Chapter 1. Philosophy") we quoted Ken Thompson: "When in doubt, use brute force". Thompson[]{#id2915308 .indexterm} understood the full cost of complicated algorithms --- not just that they\'re more bug-prone when initially implemented, but that they\'re harder for maintainers down the line to understand.

Another important practice is the inclusion of hacker\'s guides. It has always been highly approved behavior for source code distributions to include guide documents informally describing the key data structures and algorithms in the code. In fact, Unix programmers have often been better about producing hacker\'s guides than they are about writing end-user documentation.

The open-source community has seized on and elaborated this custom. Besides being advice to future maintainers, hacker\'s guides for open-source projects are also designed to make it easy for casual contributors to add features or fix bugs. The Design Notes file shipped with *fetchmail*[]{#id2915346 .indexterm} is representative. The Linux[]{#id2915354 .indexterm} kernel sources include literally dozens of these.

In [Chapter 19](http://www.catb.org/~esr/writings/taoup/html/opensourcechapter.html "Chapter 19. Open Source") we\'ll describe conventions that Unix developers have evolved for making source code distributions easy to examine and easy to build running code from. These practices, too, promote maintainability.
:::::

::: navfooter

------------------------------------------------------------------------

  ------------------------------------------------- ----------------------------------------------- --------------------------------------------------
  [Prev](ch06s02.html){accesskey="p"}                [Up](transparencychapter.html){accesskey="u"}     [Next](multiprogramchapter.html){accesskey="n"}
  Designing for Transparency and Discoverability           [Home](index.html){accesskey="h"}                               Chapter 7. Multiprogramming
  ------------------------------------------------- ----------------------------------------------- --------------------------------------------------
:::
