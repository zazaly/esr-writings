::: navheader
  Applying Unix Interface-Design Patterns                            
  ----------------------------------------- ------------------------ --------------------------------------
  [Prev](ch11s06.html){accesskey="p"}        Chapter 11. Interfaces     [Next](ch11s08.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2960113}Applying Unix Interface-Design Patterns {#applying-unix-interface-design-patterns .title style="clear: both"}

</div>
::::

To facilitate scripting and pipelining (see [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming")) it is wise to choose the simplest interface pattern possible --- that is, the pattern with the fewest channels to the environment and the least interactivity.

In many of the single-component patterns described above, it is emphasized that the pattern does not require user interaction after startup time. When the 'user' is often expected to be another program (and thus to lack the range and flexibility of a human brain) this is a very valuable feature, maximizing scriptability.

We\'ve seen that different interface design patterns optimize for traits valuable in differing circumstances. In particular, there is a strong and inherent tension between the GUIs and design patterns appropriate for novice and nontechnical end-users (on the one hand) and those which serve expert users and maximize scriptability (on the other).

One way around this dilemma is to make programs with modes that exhibit more than one pattern. An excellent example is the Web browser lynx(1). It normally has a roguelike interface for interactive use, but can be called with a `-dump` option that makes it into a source, formatting a specified Web page to text dumped on standard output.

Such dual-mode interfaces, however, are not normally attempted when the program has to have a true GUI. The reasons for this are partly historical, but mostly have to do with controlling global complexity. GUIs tend to require complex startup configurations and large volumes of specialized code; these features coexist uneasily with the simpler patterns. In the worst case, a dual-mode GUI/non-GUI program could require two separate command-interpreter loops, with all that implies in the way of code bloat and potential inconsistencies.

Thus, when "choose the simplest pattern" conflicts with a requirement to produce a GUI, the Unix way is to split the program in two, applying the 'separated engine and interface' design pattern.

In fact, by combining a theme from [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming") with this idea, we can perhaps name a new design pattern emerging under Linux[]{#id2960215 .indexterm} and other modern, open-source Unixes where GUIs are not merely a reluctant add-on but an active focus of lots of development effort.

:::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2960228}The Polyvalent-Program Pattern {#the-polyvalent-program-pattern .title}

</div>
::::

A polyvalent program has the following traits:

::: orderedlist
1.  The program\'s application-domain logic lives in a library with a documented API, which can be linked to other programs. The program\'s interface logic to the rest of the world is a thin layer over the library. Or perhaps there are several layers with different UI styles, any of which the library can be linked to.

2.  One UI mode is a cantrip, compiler-like or CLI pattern that executes its interactive commands in batch mode.

3.  One UI mode is a GUI, either linked directly to the core library or acting as as a separate process driving the CLI interface.

4.  One UI mode is a scripting interface using a modern general-purpose scripting language like Perl[]{#id2960280 .indexterm}, Python[]{#id2960288 .indexterm}, or Tcl[]{#id2960296 .indexterm}.

5.  Optional extra: One UI mode is a roguelike interface using curses(3).
:::

:::: figure
[]{#id2960323}

**Figure 11.4. Caller/callee relationships in a polyvalent program.**

::: mediaobject
![Caller/callee relationships in a polyvalent program.](http://www.catb.org/~esr/writings/taoup/html/graphics/polyvalent.png)
:::
::::

Notably, the GIMP[]{#id2960378 .indexterm} actually fulfills this pattern.
::::::::
:::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- -------------------------------------------- -------------------------------------------
  [Prev](ch11s06.html){accesskey="p"}     [Up](interfacechapter.html){accesskey="u"}          [Next](ch11s08.html){accesskey="n"}
  Unix Interface Design Patterns              [Home](index.html){accesskey="h"}          The Web Browser as a Universal Front End
  -------------------------------------- -------------------------------------------- -------------------------------------------
:::
