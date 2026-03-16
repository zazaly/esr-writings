::: navheader
  Choosing an X Toolkit                                          
  -------------------------------------- ----------------------- ----------------------------------------------------------------------------------------
  [Prev](ch14s05.html){accesskey="p"}     Chapter 14. Languages     [Next](http://www.catb.org/~esr/writings/taoup/html/toolschapter.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2978671}Choosing an X Toolkit {#choosing-an-x-toolkit .title style="clear: both"}

</div>
::::

An issue related to choice of language is choice of X toolkit for GUI programming. Recall the discussion in [Chapter 1](philosophychapter.html "Chapter 1. Philosophy") of how X separates mechanism from policy. Each possible choice of toolkit will give you a slightly different look and feel.

Your choice of X toolkit will be connected to your choice of application language in two ways: first, because some languages ship with a binding to a preferred toolkit, and second because some toolkits only have bindings to a limited set of languages.

Java[]{#id2978702 .indexterm}, of course, has its own cross-platform toolkits built in, so your choice will be between AWT (universally deployed) and Swing (more capable, more complex, slower, and only in JDK 1.2/Java 2). The remainder of this section focuses on the other languages we have surveyed. Similarly, if you\'re using Tcl, Tk comes bundled. There probably is not a lot of point in evaluating alternatives.

The once-ubiquitous Motif toolkit is effectively dead. It couldn\'t keep up with the newer toolkits distributed without license fees or restrictions. These attracted more developer effort until they surged past closed-source toolkits in capability and features; nowadays, the competition is all in open source.

The four toolkits to consider seriously in 2003 are Tk, GTK, Qt, and wxWindows, with GTK and Qt being the clear front runners. All four have ports on MacOS and Windows, so any choice will give you the capability to do cross-platform development.

The Tk toolkit is the oldest of the four and has the advantage of incumbency; it\'s native in Tcl and bindings to it are shipped with the stock version of Python[]{#id2978744 .indexterm}. Libraries to provide language bindings to Tk are generally available for C[]{#id2978754 .indexterm} and C++[]{#id2978762 .indexterm}. Unfortunately, Tk also shows its age in that its standard widget set is both limited and rather ugly. On the other hand, the Tk Canvas widget has capabilities that other toolkits still match only with difficulty.

GTK began life as a replacement for Motif, and was invented to support the GIMP[]{#id2978780 .indexterm}. It is now the preferred toolkit of the GNOME project and is used by hundreds of GNOME applications. The native API is C; bindings are available for C++[]{#id2978791 .indexterm}, Perl[]{#id2978800 .indexterm}, and Python[]{#id2978808 .indexterm}, but do not ship with the stock language distributions. It\'s the only one of these four with a native C binding.

Qt is a toolkit associated with the KDE project. It is natively a C++[]{#id2978824 .indexterm} library; bindings are available for Python[]{#id2978833 .indexterm} and Perl[]{#id2978842 .indexterm} but do not ship with the stock interpreters. Qt has a reputation for having the best-designed and most expressive API of these four, but adoption was initially hindered by controversy over early versions of the Qt license and was further slowed down by the fact that a C binding was slow in coming.

wxWindows is also natively C++[]{#id2978860 .indexterm} with bindings available in Perl[]{#id2978869 .indexterm} and Python[]{#id2978878 .indexterm}. The wxWindows developers emphasize their support for cross-platform development heavily and appear to regard it as the main selling point of the toolkit. Another selling point is that wxWindows is actually a wrapper around the native (GTK, Windows, and MacOS 9) widgets on each platform, so applications written using it retain a native look and feel.

As of mid-2003 few detailed comparisons have been written, but a Web search for "X toolkit comparison" may turn up some useful hits. [Table 14.2](ch14s06.html#x_toolkits "Table 14.2. Summary of X Toolkits.") summarizes the state of play.

::: table
[]{#x_toolkits}

**Table 14.2. Summary of X Toolkits.**

  Toolkit     Native language   Shipped with   Bindings                      
  ----------- ----------------- -------------- ---------- ----- ------ ----- --------
                                               C          C++   Perl   Tcl   Python
  Tk          Tcl               Tcl, Python    Y          Y     Y      Y     Y
  GTK         C                 Gnome          Y          Y     Y      Y     Y
  Qt          C++               KDE            Y          Y     Y      Y     Y
  wxWindows   C++               ---            ---        Y     Y      Y     Y
:::

Architecturally, these libraries are all written at about the same abstraction level. GTK and Qt use a slot-and-signal apparatus for event-handling so similar that ports between them have been reported to be almost trivial. Your choice among them will probably be conditioned more by the availability of bindings to your chosen development language than anything else.
::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- -------------------------------------------- ----------------------------------------------------------------------------------------
  [Prev](ch14s05.html){accesskey="p"}     [Up](languageschapter.html){accesskey="u"}     [Next](http://www.catb.org/~esr/writings/taoup/html/toolschapter.html){accesskey="n"}
  Trends for the Future                       [Home](index.html){accesskey="h"}                                                                              Chapter 15. Tools
  -------------------------------------- -------------------------------------------- ----------------------------------------------------------------------------------------
:::
