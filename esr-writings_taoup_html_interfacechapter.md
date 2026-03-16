::: navheader
  Chapter 11. Interfaces                                   
  -------------------------------------- ----------------- --------------------------------------
  [Prev](ch10s07.html){accesskey="p"}     Part II. Design     [Next](ch11s01.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::: {.chapter lang="en"}
::::: titlepage
<div>

## []{#interfacechapter}Chapter 11. Interfaces {#chapter-11.-interfaces .title}

</div>

<div>

### *User-Interface Design Patterns in the Unix Environment* {#user-interface-design-patterns-in-the-unix-environment .subtitle}

</div>
:::::

::: toc
**Table of Contents**

[Applying the Rule of Least Surprise](ch11s01.html)

[History of Interface Design on Unix](ch11s02.html)

[Evaluating Interface Designs](ch11s03.html)

[Tradeoffs between CLI and Visual Interfaces](ch11s04.html)

[Case Study: Two Ways to Write a Calculator Program](ch11s04.html#id2951734)

[Transparency, Expressiveness, and Configurability](ch11s05.html)

[Unix Interface Design Patterns](ch11s06.html)

[The Filter Pattern](ch11s06.html#id2957637)

[The Cantrip Pattern](ch11s06.html#id2957916)

[The Source Pattern](ch11s06.html#id2958032)

[The Sink Pattern](ch11s06.html#id2958116)

[The Compiler Pattern](ch11s06.html#id2958199)

[The ed pattern](ch11s06.html#id2958336)

[The Roguelike Pattern](ch11s06.html#id2958491)

[The 'Separated Engine and Interface' Pattern](ch11s06.html#id2958899)

[The CLI Server Pattern](ch11s06.html#id2959821)

[Language-Based Interface Patterns](ch11s06.html#id2959928)

[Applying Unix Interface-Design Patterns](ch11s07.html)

[The Polyvalent-Program Pattern](ch11s07.html#id2960228)

[The Web Browser as a Universal Front End](ch11s08.html)

[Silence Is Golden](ch11s09.html)
:::

::: {.epigraph xmlns=""}

All our knowledge has its origins in our perceptions.

\--*[ [Leonardo Da Vinci]{.author} ]{.attribution xmlns="http://www.w3.org/1999/xhtml"}*
:::

The interface of a program is the sum of all the ways that it communicates with human users and other programs. In [Chapter 10](configurationchapter.html "Chapter 10. Configuration"), we discussed the use of environment variables, switches, run-control files and other parts of start-up-time interfaces. In this chapter, we\'ll untangle the history and explain the pragmatics of Unix interfaces after startup time. Because user-interface code normally consumes 40% or more of development time, knowing good design patterns is especially important here in order to avoid a lot of false starts and time-intensive rewrites.

In the Unix tradition of interface design, we encounter two themes over and over again. One is anticipatory design for communication with other programs; the other is the Rule of Least Surprise.

Unix programs can give you extra power from being used in synergistic combinations; we discussed various methods for hooking together such combinations in [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming"). The 'other programs' part of Unix interface design is not an afterthought or a marginal case as it is under many other operating systems. Rather, it is a central challenge that has to be balanced and integrated carefully with the demands of interface design for human users.

Much of Unix-community tradition about program interface design may seem odd and arbitrary --- or even, in the age of the GUI, downright regressive --- when you encounter that tradition for the first time. But in spite of various blemishes and irregularities, that tradition has an inner logic to it which is worth learning and understanding. It reflects heuristics accumulated over Unix\'s long history about ways to do effective communication both with human beings and with other programs. And it includes a set of conventions which create commonalities between programs --- it defines 'least surprising' alternatives for a wide range of common interface-design problems.

After startup, programs normally get input or commands from the following sources:

::: itemizedlist
-   Data and commands presented on the program\'s standard input.

-   Inputs passed through IPC, such as X server events and network messages.

-   Files and devices in known locations (such as a data file name passed to or computed by the program).
:::

Programs can emit results in all the same ways (with output going to standard output).

Some Unix programs are graphical, some have screen-oriented character interfaces, and some use a starkly simple text-filter design unchanged from the days of mechanical teletypes. To the uninitiated, it is often far from obvious why any given program uses the style it does --- or, indeed, why Unix supports such a plethora of interface styles at all.

Unix has several competing interface styles. All are still alive for a reason; they\'re optimized for different situations. By understanding the fit between task and interface style, you will learn how to choose the right styles for the jobs you need to do.
:::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------- --------------------------------------
  [Prev](ch10s07.html){accesskey="p"}     [Up](design.html){accesskey="u"}      [Next](ch11s01.html){accesskey="n"}
  On Breaking These Rules                 [Home](index.html){accesskey="h"}     Applying the Rule of Least Surprise
  -------------------------------------- ----------------------------------- --------------------------------------
:::
