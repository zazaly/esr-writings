::: navheader
  Conventions Used in This Book                    
  -------------------------------------- --------- --------------------------------------
  [Prev](pr01s03.html){accesskey="p"}     Preface     [Next](pr01s05.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2807915}Conventions Used in This Book {#conventions-used-in-this-book .title style="clear: both"}

</div>
::::

The term "UNIX" is technically and legally a trademark of The Open Group, and should formally be used only for operating systems which are certified to have passed The Open Group\'s elaborate standards-conformance tests. In this book we use "Unix" in the looser sense widely current among programmers, to refer to any operating system (whether formally Unix-branded or not) that is either genetically descended from Bell Labs\'s ancestral Unix code or written in close imitation of its descendants. In particular, Linux (from which we draw most of our examples) is a Unix under this definition.

This book employs the Unix manual page convention of tagging Unix facilities with a following manual section in parentheses, usually on first introduction when we want to emphasize that this is a Unix command. Thus, for example, read "munger(1)" as "the 'munger' program, which will be documented in section 1 (user tools) of the Unix manual pages, if it\'s present on your system". Section 2 is C system calls, section 3 is C library calls, section 5 is file formats and protocols, section 8 is system administration tools. Other sections vary among Unixes but are not cited in this book. For more, type **man 1 man** at your Unix shell prompt (older System V Unixes may require **man -s 1 man**).

Sometimes we mention a Unix application (such as *Emacs*), without a manual-section suffix and capitalized. This is a clue that the name actually represents a well-established family of Unix programs with essentially the same function, and we are discussing generic properties of all of them. *Emacs*, for example, includes *xemacs*.

At various points later in this book we refer to 'old school' and 'new school' methods. As with rap music, new-school starts about 1990. In this context, it\'s associated with the rise of scripting languages[]{#id2808006 .indexterm}, GUIs, open-source Unixes, and the Web. Old-school refers to the pre-1990 (and especially pre-1985) world of expensive (shared) computers, proprietary Unixes, scripting in shell, and C everywhere. This difference is worth pointing out because cheaper and less memory-constrained machines have wrought some significant changes on the Unix programming style.
:::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------- --------------------------------------
  [Prev](pr01s03.html){accesskey="p"}     [Up](preface.html){accesskey="u"}     [Next](pr01s05.html){accesskey="n"}
  Related References                      [Home](index.html){accesskey="h"}                        Our Case Studies
  -------------------------------------- ----------------------------------- --------------------------------------
:::
