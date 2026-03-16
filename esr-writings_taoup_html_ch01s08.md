::: navheader
  Applying the Unix Philosophy                                   
  -------------------------------------- ----------------------- --------------------------------------
  [Prev](ch01s07.html){accesskey="p"}     Chapter 1. Philosophy     [Next](ch01s09.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2879244}Applying the Unix Philosophy {#applying-the-unix-philosophy .title style="clear: both"}

</div>
::::

These philosophical principles aren\'t just vague generalities. In the Unix world they come straight from experience and lead to specific prescriptions, some of which we\'ve already developed above. Here\'s a by no means exhaustive list:

::: itemizedlist
-   Everything that can be a source- and destination-independent filter [*should*]{.emphasis} be one.

-   Data streams should if at all possible be textual (so they can be viewed and filtered with standard tools).

-   Database layouts and application protocols should if at all possible be textual (human-readable and human-editable).

-   Complex front ends (user interfaces) should be cleanly separated from complex back ends.

-   Whenever possible, prototype in an interpreted language before coding C.

-   Mixing languages is better than writing everything in one, if and only if using only that one is likely to overcomplicate the program.

-   Be generous in what you accept, rigorous in what you emit.

-   When filtering, never throw away information you don\'t need to.

-   Small is beautiful. Write programs that do as little as is consistent with getting the job done.
:::

We\'ll see the Unix design rules, and the prescriptions that derive from them, applied over and over again in the remainder of this book. Unsurprisingly, they tend to converge with the very best practices from software engineering in other traditions.^\[[12](ch01s08.html#ftn.id2879339){#id2879339}\]^

:::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[12](ch01s08.html#id2879339){#ftn.id2879339}\]^ One notable example is Butler Lampson\'s *Hints for Computer System Design* \[[Lampson](http://www.catb.org/~esr/writings/taoup/html/apb.html#Lampson "[Lampson]")\], which I discovered late in the preparation of this book. It not only expresses a number of Unix dicta in forms that were clearly discovered independently, but uses many of the same tag lines to illustrate them.
:::
::::
::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- --------------------------------------------- --------------------------------------
  [Prev](ch01s07.html){accesskey="p"}     [Up](philosophychapter.html){accesskey="u"}     [Next](ch01s09.html){accesskey="n"}
  The Unix Philosophy in One Lesson            [Home](index.html){accesskey="h"}                         Attitude Matters Too
  -------------------------------------- --------------------------------------------- --------------------------------------
:::
