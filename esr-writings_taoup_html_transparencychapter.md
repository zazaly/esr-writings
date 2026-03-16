::: navheader
  Chapter 6. Transparency                                  
  -------------------------------------- ----------------- --------------------------------------
  [Prev](ch05s04.html){accesskey="p"}     Part II. Design     [Next](ch06s01.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::::: {.chapter lang="en"}
::::: titlepage
<div>

## []{#transparencychapter}Chapter 6. Transparency {#chapter-6.-transparency .title}

</div>

<div>

### *Let There Be Light* {#let-there-be-light .subtitle}

</div>
:::::

::: toc
**Table of Contents**

[Studying Cases](ch06s01.html)

[Case Study: audacity](ch06s01.html#audacity)

[Case Study: fetchmail\'s -v option](ch06s01.html#fetchmail_v)

[Case Study: GCC](ch06s01.html#id2909841)

[Case Study: kmail](ch06s01.html#id2909954)

[Case Study: SNG](ch06s01.html#id2910193)

[Case Study: The Terminfo Database](ch06s01.html#id2910334)

[Case Study: Freeciv Data Files](ch06s01.html#id2914115)

[Designing for Transparency and Discoverability](ch06s02.html)

[The Zen of Transparency](ch06s02.html#zen_of_transparency)

[Coding for Transparency and Discoverability](ch06s02.html#id2914509)

[Transparency and Avoiding Overprotectiveness](ch06s02.html#id2914680)

[Transparency and Editable Representations](ch06s02.html#id2914758)

[Transparency, Fault Diagnosis, and Fault Recovery](ch06s02.html#id2915107)

[Designing for Maintainability](ch06s03.html)
:::

[]{#id2909441 .indexterm}

::: {.epigraph xmlns=""}

Beauty is more important in computing than anywhere else in technology because software is so complicated. Beauty is the ultimate defense against complexity.

\--*[ [David Gelernter]{.author} *Machine Beauty: Elegance and the Heart of Technology (1998)* []{#id2911430 .indexterm} ]{.attribution xmlns="http://www.w3.org/1999/xhtml"}*
:::

In the previous chapter we discussed the importance of textual data formats and application protocols, representations that are easy for human beings to examine and interact with. These promote qualities in design that are much valued in the Unix tradition but seldom if ever talked about explicitly: *transparency*[]{#id2911463 .indexterm} and *discoverability*.

Software systems are transparent when they don\'t have murky corners or hidden depths. Transparency is a passive quality. A program is transparent when it is possible to form a simple mental model of its behavior that is actually predictive for all or most cases, because you can see through the machinery to what is actually going on.

Software systems are discoverable when they include features that are designed to help you build in your mind a correct mental model of what they do and how they work. So, for example, good documentation helps discoverability to a user. Good choice of variable and function names helps discoverability to a programmer. Discoverability[]{#id2911497 .indexterm} is an active quality. To achieve it in your software you cannot merely fail to be obscure, you have to go out of your way to be helpful.^\[[58](transparencychapter.html#ftn.id2911508){#id2911508}\]^

Transparency and discoverability are important for both users and software developers. But they\'re important in different ways. Users like these properties in a UI because they mean an easier learning curve. UI transparency and discoverability are a large part of what people mean when they say a UI is 'intuitive'; most of the rest is the Rule of Least Surprise. We\'ll examine the properties that make user interfaces pleasant and effective in more depth in [Chapter 11](interfacechapter.html "Chapter 11. Interfaces").

Software developers like these qualities in the code itself (the part users don\'t see) because they so often need to understand it well enough to modify and debug it. Also, a program designed so that its internal data flows are readily comprehensible is more likely to be one that does not fail because of bad interactions that the designer didn\'t notice, and more likely to be able to evolve forward gracefully (including accommodating change when new maintainers pick up the baton).

Transparency is a major component of what David Gelernter[]{#id2911563 .indexterm} refers to as "beauty" in this chapter\'s epigraph. Unix programmers, borrowing from mathematicians, often use the more specific term "elegance" for the quality Gelernter speaks of. Elegance is a combination of power and simplicity. Elegant code does much with little. Elegant code is not only correct but visibly, [*transparently*]{.emphasis} correct. It does not merely communicate an algorithm to a computer, but also conveys insight and assurance to the mind of a human that reads it. By seeking elegance in our code, we build better code. Learning to write transparent code is a first, long step toward learning how to write elegant code --- and taking care to make code discoverable helps us learn how to make it transparent. Elegant code is both transparent and discoverable.

It may be easier to appreciate the difference between transparency and discoverability with a pair of extreme examples. The Linux[]{#id2911604 .indexterm} kernel source is remarkably transparent (given the intrinsic complexity of what it does) but not at all discoverable --- acquiring the minimum knowledge needed to live in the code and understand the idiom of the developers is difficult, but once you do the whole makes sense.^\[[59](transparencychapter.html#ftn.id2911617){#id2911617}\]^ On the other hand, the Emacs Lisp libraries are discoverable but not transparent. It\'s easy to acquire enough knowledge to tweak just one thing, but quite difficult to comprehend the whole system.

In this chapter, we\'ll examine features of Unix designs that promote transparency and discoverability not just in UIs but in the parts users don\'t normally see. We\'ll develop some useful rules you can apply to your coding and development practice. Later on, in [Chapter 19](http://www.catb.org/~esr/writings/taoup/html/opensourcechapter.html "Chapter 19. Open Source") we\'ll see how good release-engineering practices (like having a `README` file with appropriate content) can make your source code as discoverable as your design.

If you need a practical reminder why these qualities are important, remember that the sanity you save by writing transparent, discoverable systems may well be that of your own future self.

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[58](transparencychapter.html#id2911508){#ftn.id2911508}\]^ An economically-minded friend comments: "Discoverability is about reducing barriers to entry; transparency is about reducing the cost of living in the code".
:::

::: footnote
^\[[59](transparencychapter.html#id2911617){#ftn.id2911617}\]^ The Linux kernel makes a number of attempts at discoverability, including the Documentation subdirectory in the Linux kernel source tarball and quite a number of tutorial websites and books. These attempts are frustrated by the speed at which the kernel changes; the documentation has a chronic tendency to fall behind.
:::
:::::
:::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------- --------------------------------------
  [Prev](ch05s04.html){accesskey="p"}     [Up](design.html){accesskey="u"}      [Next](ch06s01.html){accesskey="n"}
  Application Protocol Metaformats        [Home](index.html){accesskey="h"}                          Studying Cases
  -------------------------------------- ----------------------------------- --------------------------------------
:::
