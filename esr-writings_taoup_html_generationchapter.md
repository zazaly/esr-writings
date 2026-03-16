::: navheader
  Chapter 9. Generation                                    
  -------------------------------------- ----------------- --------------------------------------
  [Prev](ch08s03.html){accesskey="p"}     Part II. Design     [Next](ch09s01.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::::: {.chapter lang="en"}
::::: titlepage
<div>

## []{#generationchapter}Chapter 9. Generation {#chapter-9.-generation .title}

</div>

<div>

### *Pushing the Specification Level Upwards* {#pushing-the-specification-level-upwards .subtitle}

</div>
:::::

::: toc
**Table of Contents**

[Data-Driven Programming](ch09s01.html)

[Case Study: ascii](ch09s01.html#id2939746)

[Case Study: Statistical Spam Filtering](ch09s01.html#bayes_spam)

[Case Study: Metaclass Hacking in fetchmailconf](ch09s01.html#fetchmailconf)

[Ad-hoc Code Generation](ch09s02.html)

[Case Study: Generating Code for the ascii Displays](ch09s02.html#id2938615)

[Case Study: Generating HTML Code for a Tabular List](ch09s02.html#htmlgen)
:::

::: {.epigraph xmlns=""}

The programmer at wit\'s end \... can often do best by disentangling himself from his code, rearing back, and contemplating his data. Representation is the essence of programming.

\--*[ [Fred Brooks]{.author} *The Mythical Man-Month, Anniversary Edition (1975-1995), p. 103* []{#id2939500 .indexterm} ]{.attribution xmlns="http://www.w3.org/1999/xhtml"}*
:::

In [Chapter 1](philosophychapter.html "Chapter 1. Philosophy") we observed that human beings are better at visualizing data than they are at reasoning about control flow. We recapitulate: To see this, compare the expressiveness and explanatory power of a diagram of a fifty-node pointer tree with a flowchart of a fifty-line program. Or (better) of an array initializer expressing a conversion table with an equivalent switch statement. The difference in transparency[]{#id2939533 .indexterm} and clarity is dramatic.^\[[97](generationchapter.html#ftn.id2939543){#id2939543}\]^

Data is more tractable than program logic. That\'s true whether the data is an ordinary table, a declarative markup language, a templating system, or a set of macros that will expand to program logic. It\'s good practice to move as much of the complexity in your design as possible away from procedural code and into data, and good practice to pick data representations that are convenient for humans to maintain and manipulate. Translating those representations into forms that are convenient for machines to process is another job for machines, not for humans.

::: blockquote
  ------------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                            Another important advantage of higher-level, more declarative notations is that they lend themselves better to compile-time checking. Procedural notations inherently have complex runtime behavior which is difficult to analyze at compile time. Declarative notations give the implementation much more leverage for finding mistakes, by permitting much more thorough understanding of the intended behavior.    
  \--[ [Henry Spencer]{.author} []{#id2939580 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                         
  ------------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

These insights ground in theory a set of practices that have always been an important part of the Unix programmer\'s toolkit --- very high-level languages, data-driven programming, code generators, and domain-specific minilanguages. What unifies these is that they are all ways of lifting the generation of code up some levels, so that specifications can be smaller. We\'ve previously noted that defect densities tend to be nearly constant across programming languages; all these practices mean that whatever malign forces generate our bugs will get fewer lines to wreak their havoc on.

In [Chapter 8](minilanguageschapter.html "Chapter 8. Minilanguages") we discussed the uses of domain-specific minilanguages. In [Chapter 14](languageschapter.html "Chapter 14. Languages") we\'ll make the argument for very-high-level languages[]{#id2939637 .indexterm}. In this chapter we\'ll look at some design studies in data-driven programming and a few examples of ad-hoc code generation; we\'ll look at some code-generation tools in [Chapter 15](http://www.catb.org/~esr/writings/taoup/html/toolschapter.html "Chapter 15. Tools"). As with minilanguages, these methods can enable you to drastically cut the line count of your programs, and correspondingly lower debugging time and maintenance costs.

:::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[97](generationchapter.html#id2939543){#ftn.id2939543}\]^ For further development of this point see \[[Bentley](http://www.catb.org/~esr/writings/taoup/html/apb.html#Bentley "[Bentley]")\].
:::
::::
:::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------- --------------------------------------
  [Prev](ch08s03.html){accesskey="p"}     [Up](design.html){accesskey="u"}      [Next](ch09s01.html){accesskey="n"}
  Designing Minilanguages                 [Home](index.html){accesskey="h"}                 Data-Driven Programming
  -------------------------------------- ----------------------------------- --------------------------------------
:::
