::: navheader
  What Should Be Configurable?                                                    
  --------------------------------------------------- --------------------------- --------------------------------------
  [Prev](configurationchapter.html){accesskey="p"}     Chapter 10. Configuration     [Next](ch10s02.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2943724}What Should Be Configurable? {#what-should-be-configurable .title style="clear: both"}

</div>
::::

Before plunging into the details of different kinds of program configuration, we should ask a high-level question: What things should be configurable?

The gut-level Unix answer is "everything". The Rule of Separation that we discussed in [Chapter 1](philosophychapter.html "Chapter 1. Philosophy") encourages Unix programmers to build mechanism and defer policy decisions outward toward the user wherever possible. While this tends to produce programs that are powerful and rewarding for expert users, it also tends to produce interfaces that overwhelm novices and casual users with a surfeit of choices, and with configuration files sprouting like weeds.

Unix programmers aren\'t going to be cured of their tendency to design for their peers and the most sophisticated users any time soon (we\'ll grapple a bit with the question of whether such a change would actually be desirable in [Chapter 20](http://www.catb.org/~esr/writings/taoup/html/futurechapter.html "Chapter 20. Futures")). So it\'s perhaps more useful to invert the question and ask "What things should [*not*]{.emphasis} be configurable?" Unix practice does offer some guidelines on this.

First, [*don\'t provide configuration switches for what you can reliably detect automatically*]{.emphasis}. This is a surprisingly common mistake. Instead, look for ways to eliminate configuration switches by autodetection, or by trying alternative methods at runtime until one succeeds. If this strikes you as inelegant or too expensive, ask yourself if you haven\'t fallen into premature optimization.

::: blockquote
  ------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                            One of the nicest examples of autodetection I experienced was when Dennis Ritchie and I were porting Unix to the Interdata 8/32. This was a big-endian machine, and we had to generate data for that machine on a PDP-11, write a magnetic tape, and then load the magnetic tape on the Interdata. A common error was to forget to twiddle the byte order; a checksum error showed you that you had to unmount, remount again on the PDP-11, regenerate the tape, unmount, and remount. Then one day Dennis hacked the Interdata tape reader program so that if it got a checksum error it rewound the tape, toggled 'byte flip' switch and reread it. A second checksum error would kill the load, but 99% of the time it just read the tape and did the right thing. Our productivity shot up, and we pretty much ignored tape byte order from that point on.    
  \--[ [Steve Johnson]{.author} []{#id2943810 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      
  ------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

A good rule of thumb is this: Be adaptive unless doing so costs you 0.7 seconds or more of latency. 0.7 seconds is a magic number because, as Jef Raskin discovered while designing the Canon Cat, humans are almost incapable of noticing startup latency shorter than that; it gets lost in the mental overhead of changing the focus of attention.

Second, [*users should not see optimization switches*]{.emphasis}. As a designer, it\'s [*your*]{.emphasis} job to make the program run economically, not the user\'s. The marginal gains in performance that a user might collect from optimization switches are usually not worth the interface-complexity cost.

::: blockquote
  ------------------------------------------------------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                           File-format nonsense (record length, blocking factor, etc) was blessedly eschewed by Unix, but the same kind of thing has roared back in excess configuration goo. KISS became MICAHI: make it complicated and hide it.    
  \--[ [Doug McIlroy]{.author} []{#id2943882 .indexterm} ]{.attribution}                                                                                                                                                                                                                              
  ------------------------------------------------------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Finally, [*don\'t do with a configuration switch what can be done with a script wrapper or a trivial pipeline*]{.emphasis}. Don\'t put complexity inside your program when you can easily enlist other programs to help get the work done. (Recall our discussion in [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming") of why ls(1) does not have a built-in pager, or an option to invoke it).

Here are some more general questions to consider whenever you find yourself thinking about adding a configuration option:

::: itemizedlist
-   Can I leave this feature out? Why am I fattening the manual and burdening the user?

-   Could the program\'s normal behavior be changed in an innocuous way that would make the option unnecessary?

-   Is this option merely cosmetic? Should I be thinking less about how to make the user interface configurable and more about how to make it right?

-   Should the behavior enabled by this option be a separate program instead?
:::

Proliferating unnecessary options has many bad effects. One of the subtlest but most serious is what it will do to your test coverage.

::: blockquote
  ------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                            Unless it is done very carefully, the addition of an on/off configuration option can lead to a need to double the amount of testing. Since in practice one never does double the amount of testing, the practical effect is to reduce the amount of testing that any given configuration receives. Ten options leads to 1024 times as much testing, and pretty soon you are talking real reliability problems.    
  \--[ [Steve Johnson]{.author} []{#id2943989 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                     
  ------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::
:::::::::

::: navfooter

------------------------------------------------------------------------

  --------------------------------------------------- ------------------------------------------------ --------------------------------------
  [Prev](configurationchapter.html){accesskey="p"}     [Up](configurationchapter.html){accesskey="u"}     [Next](ch10s02.html){accesskey="n"}
  Chapter 10. Configuration                                  [Home](index.html){accesskey="h"}                      Where Configurations Live
  --------------------------------------------------- ------------------------------------------------ --------------------------------------
:::
