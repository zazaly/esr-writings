::: navheader
  Chapter 13. Complexity                                   
  -------------------------------------- ----------------- --------------------------------------
  [Prev](ch12s04.html){accesskey="p"}     Part II. Design     [Next](ch13s01.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::: {.chapter lang="en"}
::::: titlepage
<div>

## []{#complexitychapter}Chapter 13. Complexity {#chapter-13.-complexity .title}

</div>

<div>

### *As Simple As Possible, but No Simpler* {#as-simple-as-possible-but-no-simpler .subtitle}

</div>
:::::

::: toc
**Table of Contents**

[Speaking of Complexity](ch13s01.html)

[The Three Sources of Complexity](ch13s01.html#id2964646)

[Tradeoffs between Interface and Implementation Complexity](ch13s01.html#id2964843)

[Essential, Optional, and Accidental Complexity](ch13s01.html#id2961759)

[Mapping Complexity](ch13s01.html#id2961870)

[When Simplicity Is Not Enough](ch13s01.html#id2963237)

[A Tale of Five Editors](ch13s02.html)

[ed](ch13s02.html#id2963445)

[vi](ch13s02.html#vi_complexity)

[Sam](ch13s02.html#id2963798)

[Emacs](ch13s02.html#emacs_editing)

[Wily](ch13s02.html#id2967110)

[The Right Size for an Editor](ch13s03.html)

[Identifying the Complexity Problems](ch13s03.html#id2967267)

[Compromise Doesn\'t Work](ch13s03.html#id2967642)

[Is Emacs an Argument against the Unix Tradition?](ch13s03.html#id2967765)

[The Right Size of Software](ch13s04.html)
:::

::: {.epigraph xmlns=""}

Everything should be made as simple as possible, but no simpler.

\--*[ [Albert Einstein]{.author} []{#id2964548 .indexterm} ]{.attribution xmlns="http://www.w3.org/1999/xhtml"}*
:::

At the end of [Chapter 1](philosophychapter.html "Chapter 1. Philosophy"), we summarized the Unix philosophy as "Keep It Simple, Stupid!" Throughout the Design section, one of the continuing themes has been the importance of keeping designs and implementations as simple as possible. But what [*is*]{.emphasis} "as simple as possible"? How do you tell?

We\'ve held off on addressing this question until now because understanding simplicity is complicated. It needs some of the ideas we developed earlier in the Design section, especially in [Chapter 4](modularitychapter.html "Chapter 4. Modularity") and [Chapter 11](interfacechapter.html "Chapter 11. Interfaces"), as background.

The large questions in this chapter are central preoccupations of the Unix tradition, some of them motivating holy wars that have simmered for decades. This chapter starts from established Unix practice and vocabulary, then goes a bit further beyond it than we do in the rest of the book. We don\'t try to develop simple answers to these questions, because there aren\'t any --- but we can hope that you will walk away with better conceptual tools for developing your own answers.
::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------- --------------------------------------
  [Prev](ch12s04.html){accesskey="p"}     [Up](design.html){accesskey="u"}      [Next](ch13s01.html){accesskey="n"}
  Throughput vs. Latency                  [Home](index.html){accesskey="h"}                  Speaking of Complexity
  -------------------------------------- ----------------------------------- --------------------------------------
:::
