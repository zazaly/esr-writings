::: navheader
  Interpreted Languages and Mixed Strategies                           
  -------------------------------------------- ----------------------- --------------------------------------
  [Prev](why_not_c.html){accesskey="p"}         Chapter 14. Languages     [Next](ch14s04.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2968378}Interpreted Languages and Mixed Strategies {#interpreted-languages-and-mixed-strategies .title style="clear: both"}

</div>
::::

Languages that avoid manual memory management do it by having a memory manager built into their runtime executable somewhere. Typically, runtime environments in these languages are split into a program part (the running script itself) and the interpreter part, with the interpreter managing dynamic storage. On Unixes (and other modern operating systems) the interpreter core can be shared by multiple program parts, reducing the effective overhead for each one.

[]{#sh_history} []{#id2968402 .indexterm} Scripting is nowhere near a new idea in the Unix world. As far back as the mid-1970s, in an era of far smaller machines, the Unix shell (the interpreter for commands typed to a Unix console) was designed as a full interpreted programming language. It was common even then to write programs entirely in shell[]{#id2968419 .indexterm}, or to use the shell to write glue logic that knit together canned utilities and custom programs in C into wholes greater than the sum of their parts. Classical introductions to the Unix environment (such as *The Unix Programming Environment* \[[Kernighan-Pike84](http://www.catb.org/~esr/writings/taoup/html/apb.html#Kernighan-Pike84 "[Kernighan-Pike84]")\]) have dwelt heavily on this tactic, and with good reason: it was one of Unix\'s most important innovations.

Advanced shell programming mixes languages freely, employing both binaries and interpreted elements from half a dozen or more other languages for subtasks. Each language does what it does best, each component is a module with narrow interfaces to the others, and the global complexity of the whole is much lower than it would be had it been coded as a single monster monolith in a general-purpose language.
:::::

::: navfooter

------------------------------------------------------------------------

  ---------------------------------------- -------------------------------------------- --------------------------------------
  [Prev](why_not_c.html){accesskey="p"}     [Up](languageschapter.html){accesskey="u"}     [Next](ch14s04.html){accesskey="n"}
  Why Not C?                                    [Home](index.html){accesskey="h"}                         Language Evaluations
  ---------------------------------------- -------------------------------------------- --------------------------------------
:::
