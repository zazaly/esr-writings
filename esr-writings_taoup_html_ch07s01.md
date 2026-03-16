::: navheader
  Separating Complexity Control from Performance Tuning                                 
  ------------------------------------------------------- ----------------------------- --------------------------------------
  [Prev](multiprogramchapter.html){accesskey="p"}          Chapter 7. Multiprogramming     [Next](ch07s02.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2918559}Separating Complexity Control from Performance Tuning {#separating-complexity-control-from-performance-tuning .title style="clear: both"}

</div>
::::

First, though, we need to dispose of a few red herrings. Our discussion is [*not*]{.emphasis} going to be about using concurrency to improve performance. Putting that concern before developing a clean architecture that minimizes global complexity is premature optimization[]{#id2918577 .indexterm}, the root of all evil (see [Chapter 12](optimizationchapter.html "Chapter 12. Optimization") for further discussion).

A closely related red herring is threads (that is, multiple concurrent processes sharing the same memory-address space). Threading is a performance hack. To avoid a long diversion here, we\'ll examine threads in more detail at the end of this chapter; the summary is that they do not reduce global complexity but rather [*increase*]{.emphasis} it, and should therefore be avoided save under dire necessity.

Respecting the Rule of Modularity, on the other hand, is [*not*]{.emphasis} a red herring; doing so can make your programs --- and your life --- simpler. All the reasons for process partitioning are continuous with the reasons for module partitioning that we developed in [Chapter 4](modularitychapter.html "Chapter 4. Modularity").

Another important reason for breaking up programs into cooperating processes is for better security. Under Unix, programs that must be run by ordinary users, but must have write access to security-critical system resources, get that access through a feature called the *setuid bit*.^\[[66](ch07s01.html#ftn.id2915417){#id2915417}\]^ Executable files are the smallest unit of code that can hold a setuid bit; thus, every line of code in a setuid executable must be trusted. (Well-written setuid programs, however, take all necessary privileged actions first and then drop their privileges back to user level for the remainder of their existence.)

Usually a setuid program only needs its privileges for one or a small handful of operations. It is often possible to break up such a program into cooperating processes, a smaller one that needs setuid and a larger one that does not. When we can do this, only the code in the smaller program has to be trusted. It is in significant part because this kind of partitioning and delegation is possible that Unix has a better security track record^\[[67](ch07s01.html#ftn.id2915447){#id2915447}\]^ than its competitors.

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[66](ch07s01.html#id2915417){#ftn.id2915417}\]^ A setuid program runs not with the privileges of the user calling it, but with the privileges of the owner of the executable. This feature can be used to give restricted, program-controlled access to things like the password file that nonadministrators should not be allowed to modify directly.
:::

::: footnote
^\[[67](ch07s01.html#id2915447){#ftn.id2915447}\]^ That is, a better record measured in security breaches per total machine hours of Internet exposure.
:::
:::::
::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------------------- ----------------------------------------------- --------------------------------------
  [Prev](multiprogramchapter.html){accesskey="p"}     [Up](multiprogramchapter.html){accesskey="u"}     [Next](ch07s02.html){accesskey="n"}
  Chapter 7. Multiprogramming                               [Home](index.html){accesskey="h"}                  Taxonomy of Unix IPC Methods
  -------------------------------------------------- ----------------------------------------------- --------------------------------------
:::
