::: navheader
  Speaking of Complexity                                                    
  ------------------------------------------------ ------------------------ --------------------------------------
  [Prev](complexitychapter.html){accesskey="p"}     Chapter 13. Complexity     [Next](ch13s02.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::::::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2964620}Speaking of Complexity {#speaking-of-complexity .title style="clear: both"}

</div>
::::

As with previous issues about modularity and interface design, Unix programmers react to a set of distinctions they have often learned from experience without knowing how to articulate. Therefore we\'ll need to start by developing some terminology.

We will start by defining what software complexity is. We will make some horizontal distinctions between different flavors of complexity, which sometimes have to be traded off against each other. We will finish by making some even more important vertical distinctions, between the kinds of complexity we must live with and the kinds we have the option to eliminate.

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2964646}The Three Sources of Complexity {#the-three-sources-of-complexity .title}

</div>
::::

Questions about simplicity, complexity, and the right size of software arouse a lot of passion in the Unix world. Unix programmers have learned a view of the world in which simplicity is beauty is elegance is good, and in which complexity is ugliness is grotesquery is evil.

Underlying the Unix programmer\'s passion for simplicity is a pragmatic fact: complexity costs. Complex software is harder to think about, harder to test, harder to debug, and harder to maintain --- and above all, harder to learn and use. The costs of complexity, rough as they are during development, bite hardest after deployment. Complexity creates places for bugs to nest, from which they will emerge to trouble the world through the entire lifetime of their software.

All kinds of pressures tend to drag programmers into a swamp of complexity nevertheless. We\'ve examined a rogue\'s gallery of these in earlier chapters; feature creep and premature optimization are the two most notorious. Traditionally, Unix programmers push back against these tendencies by proclaiming with religious fervor a rhetoric that condemns all complexity as bad.

So what exactly do we mean by 'complexity'? This point is worth pinning down, because it varies by observer.

Unix programmers (like other programmers) tend to focus on *implementation complexity*---basically, the degree of difficulty a programmer will experience in attempting to understand a program so he or she can mentally model or debug it.

Customers and users, on the other hand, tend to see complexity in terms of the program\'s *interface complexity*. In [Chapter 11](interfacechapter.html "Chapter 11. Interfaces") we discussed the quality of ease and its inverse, mnemonic load. To a user, complexity correlates closely with mnemonic load. Poor expressiveness and concision can matter too, if a weak interface forces the user to perform lots of error-prone or merely tedious low-level operations rather than a few high-level ones.

Driven by both of these is a third measure that is much simpler: the total number of lines of code in the system, its *codebase size*. In terms of life-cycle costs, this is usually the most important measure. The reasons go back to perhaps the most important empirical result in software engineering, one we\'ve cited before: the defect density of code, bugs per hundred lines, tends to be a constant independent of implementation language. More lines of code means more bugs, and debugging is the most expensive and time-consuming part of development.

Codebase size, interface complexity and implementation complexity may all rise together. That is the usual result of feature creep, and why programmers especially dread it. Premature optimization doesn\'t tend to raise interface complexity, but it has bad effects (often severely bad) on implementation complexity and codebase size. But those sorts of arguments against complexity are relatively easy to win; the difficult ones begin when these three measures have to be traded off against each other.

We\'ve already mentioned one situation in which two measures vary in opposite directions: a user interface that has been designed primarily to preserve implementation simplicity, or keep codebase size down, may simply dump low-level tasks on the user. (A crude example of this, barely imaginable to a Unix programmer but all too common elsewhere, might be an editor that lacked a global-replace feature.) Though this sort of design failure is all too common, it does not traditionally have a name. We\'ll call it a *manularity trap*.

Pressure to keep the codebase size down by using extremely dense and complicated implementation techniques can cause a cascade of implementation complexity in the system, leading to an un-debuggable mess. This used to happen frequently when fitting programs onto very small systems demanded assembler programming or tricks like self-modifying code; nowadays it is uncommon except in embedded systems, and rapidly becoming rare even there. This kind of design failure doesn\'t have a traditional name, but one might call it a *blivet trap*, after an old Army term for the results of attempting to stuff ten pounds of horse manure into a five-pound bag.

The blivet trap won\'t appear in our case studies, but we\'ve defined it for contrast with its opposite. It can happen that the designers of a project are so wary of implementation complexity that they reject a complex but unified way to solve a whole class of problems in favor of lots of duplicative, ad-hoc code that solves each individual one in turn. The result is bloat in the size of the codebase, and maintainability problems more severe than if the unified method had been accepted. For example, a Web project that really needs a centralized relational database behind its pages might instead spawn several different keyed data files containing information that has to be reintegrated at page generation time. This sort of failure is all too common. It doesn\'t have a traditional name; we\'ll call it an *adhocity trap*.

These are the three faces of complexity, and some of the traps designers fall into in attempts to avoid them.^\[[114](ch13s01.html#ftn.id2964826){#id2964826}\]^ We\'ll see more examples when we get to the case studies later in the chapter.
:::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2964843}Tradeoffs between Interface and Implementation Complexity {#tradeoffs-between-interface-and-implementation-complexity .title}

</div>
::::

One of the most perceptive observations ever made about the Unix tradition by someone standing outside it was contained in Richard Gabriel\'s paper called *Lisp: Good News, Bad News, and How to Win Big* \[[Gabriel](http://www.catb.org/~esr/writings/taoup/html/apb.html#Gabriel "[Gabriel]")\]. Gabriel is a long-time leader of the Lisp community, and the paper was primarily an argument for a particular style of Lisp[]{#id2961605 .indexterm} design, but the author himself acknowledges that it is now remembered primarily for the section called 'The Rise of [*Worse Is Better*]{.emphasis}'[]{#id2961620 .indexterm}.

The paper argued that Unix and C have the characteristics of viruses, and that in the evolutionary struggle among software designs traits like implementation simplicity and portability which lead to rapid propagation (infectiousness) are more effective than correctness and completeness of the design. Gabriel came so close to anticipating the 'many-eyeballs' effect on open-source software that the open-source community retrospectively adopted him as one of its theorists after 1997.

Less remembered is that the Gabriel\'s central argument was about a very specific tradeoff between implementation and interface complexity, one which rather exactly fits the categories we have examined in this chapter. Gabriel contrasts an 'MIT' philosophy most valuing interface simplicity with a 'New Jersey' philosophy most valuing implementation simplicity. He then proposes that although the MIT philosophy leads to software that is better in the abstract, the (worse) New Jersey model has better propagation characteristics. Over time, people pay more attention to software written in the New Jersey style, so it improves faster. Worse becomes better.

In fact, the MIT and New Jersey philosophies have analogs as conflicting tendencies within the Unix design tradition itself. One strain of Unix thinking emphasizes small sharp tools, starting designs from zero, and interfaces that are simple and consistent. This point of view has been most famously championed by Doug McIlroy. Another strain emphasizes doing simple implementations that work, and that ship quickly, even if the methods are brute-force and some edge cases have to be punted. Ken Thompson\'s code and his maxims about programming have often seemed to lean in this direction.

The tension between these approaches arises precisely because one can sometimes get a simpler interface if one is willing to pay implementation complexity for it, or vice versa. Gabriel\'s original example, about how system calls that do long operations handle interrupts they cannot hold or mask, is still one of the best. Under the MIT philosophy, the right thing to do would be to back out of the system call and automatically resume it once the interrupt has been handled; this is harder to implement but leads to a simpler interface. Under the New Jersey philosophy, the system call would return an error indicating that it has been interrupted and the user must re-execute; this can be implemented far more simply, but leads to a programming interface that is more difficult to use.

Both approaches have been tried. Old Unix hands will instantly think of System-V-style vs. BSD-style handling of software signals; the latter follows the MIT philosophy, while the former hails from New Jersey. Underlying the choice between them is a pressing question that has nothing directly to do with the software\'s infectiousness: if your goal is to hold down total global complexity, where are you most willing to pay to do that? Where [*should*]{.emphasis} you be most willing to pay?

One epochal example not mentioned in Gabriel\'s paper is from distributed hypertext systems. Early distributed-hypertext projects such as NLS and Xanadu were severely constrained by the MIT-philosophy assumption that dangling links were an unacceptable breakdown in the user interface; this constrained the systems to either browsing only a controlled, closed set of documents (such as on a single CD-ROM) or implementing various increasingly elaborate replication, caching, and indexing methods in an attempt to prevent documents from randomly disappearing. Tim Berners-Lee cut through this Gordian knot by punting the problem in classic New Jersey style. The simplicity of implementation he bought by allowing "404: Not Found" as a response was what made the World Wide Web lightweight enough to propagate and succeed.

Gabriel himself, while sticking with the observation that 'worse' is more infectious and tends to win in the end, has publicly changed his mind several times about the underlying complexity-related question of whether or not this is actually a good thing. His uncertainty mirrors a lot of ongoing design debates within the Unix community.

We cannot offer a one-size-fits-all answer. As with most of the large questions in this chapter, good taste and engineering judgement will demand different answers in different situations. The important thing is to develop the habit of thinking carefully about this issue on each and every one of your designs. As we have observed before in discussing software modularity, complexity is a cost you must budget very carefully.
:::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2961759}Essential, Optional, and Accidental Complexity {#essential-optional-and-accidental-complexity .title}

</div>
::::

In an ideal world, Unix programmers would craft only small, perfect gems of software, each minimal, each elegant, each perfect. But one of the unfortunate things about reality is that it often poses complex problems that demand complex solutions. You can\'t control a jetliner with an elegant ten-line procedure. There are too many pieces of equipment, too many channels and interfaces, too many different processors --- too many different subsystems defined by independently operating human beings who often don\'t agree even on fundamental conventions. Even if you are successful at making all the individual software parts of an avionics system elegant, integration is likely to produce a large, complex, and grubby body of code with (one hopes) the single virtue that it will actually [*work*]{.emphasis}.

Jetliners have *essential complexity*. There is a rather sharp point past which it\'s not possible to trade away features for simplicity, because the plane has to stay in the air. Because of that very fact, avionics control systems do not tend to spawn religious wars about complexity --- and Unix programmers tend to stay away from them.

Jetliners are certainly not immune from system failures due to overcomplexity. But the design issues are easier to discern and think about in software for which the requirements are more flexible, in which it is easy to trade off between anticipated features and complexity. (Here, and in the rest of this chapter, we will use 'feature' in a very general sense that includes things like performance gains or overall degree of interface polish.)

To sharpen our vision, we need to begin by noticing a difference between *accidental complexity* and *optional complexity*.^\[[115](ch13s01.html#ftn.id2961828){#id2961828}\]^ Accidental complexity happens because someone didn\'t find the simplest way to implement a specified set of features. Accidental complexity can be eliminated by good design, or good redesign. Optional complexity, on the other hand, is tied to some desirable feature. Optional complexity can be eliminated only by changing the project\'s objectives.

When we fail to distinguish between optional and accidental complexity, design debates become seriously confused. Questions about what a project\'s objectives are get confused with questions about the aesthetics of simplicity, and whether people have been sufficiently clever.
:::::

::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2961870}Mapping Complexity {#mapping-complexity .title}

</div>
::::

So far, we\'ve developed two different scales for thinking about complexity. These scales are actually orthogonal to each other. [Figure 13.1](ch13s01.html#complexity-sources "Figure 13.1. Sources and kinds of complexity.") may help clarify the relationships. Each of the nine boxes of the figure lists a common source of a particular kind of complexity.

:::: figure
[]{#complexity-sources}

**Figure 13.1. Sources and kinds of complexity.**

::: mediaobject
![Sources and kinds of complexity.](http://www.catb.org/~esr/writings/taoup/html/graphics/complexity.png)
:::
::::

We\'ve touched on some of these varieties of complexity earlier in this book, especially the accidental ones. In [Chapter 4](modularitychapter.html "Chapter 4. Modularity") we saw that accidental interface complexity often comes from non-orthogonality in the interface design --- that is, failing to carefully factor the interface operations so that each does exactly one thing. Accidental code complexity (making code more complicated than it needs to be to get the job done) often results from premature optimization. Accidental codebase bloat often results from violating the SPOT rule, duplicating code or organizing it poorly so that opportunities for reuse aren\'t recognized.

Essential interface complexity usually can\'t be cut without trimming the basic functional requirements for the software (a theme we\'ll develop further in this chapter\'s case studies). Essential codebase size is related to choice of development tools because, if the feature list is held constant, the most important factor in codebase size is probably the choice of implementation language (as we implied in [Chapter 8](minilanguageschapter.html "Chapter 8. Minilanguages")).

Sources of optional complexity are the most difficult to make useful generalizations about, because they so often depend on delicate judgments about which features it is worth paying the complexity cost for. Optional interface complexity often comes from adding convenience features that make life easier for users but aren\'t essential to the function of the program. Optional increases in codebase size (supposing the user-visible features and the algorithms used are held constant) can often come from various sorts of practices intended to make it more maintainable --- adding mode comments, using long variable names, and so forth. Optional implementation complexity tends to be driven by [*everything*]{.emphasis} that touches a project.

The sources of complexity have to be grappled with in different ways. Codebase size can be attacked with better tools. Implementation complexity can be addressed with better choice of algorithms. Interface complexity has to be addressed with better interaction design, a skill involving considerations of ergonomics and user psychology. This skill is less common (and possibly more difficult) than writing code.

Attacking the kinds of complexity, on the other hand, has to be done more with insight than with methods. You cut accidental complexity by noticing that there is a simpler way to do things. You cut optional complexity by making context-dependent judgments about what features are worthwhile. You can only cut essential complexity by having an epiphany, fundamentally redefining the problem you are addressing.
:::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2963237}When Simplicity Is Not Enough {#when-simplicity-is-not-enough .title}

</div>
::::

The failure mode that goes with the Unix tradition\'s insistence on simplicity is that Unix programmers often talk (and sometimes even behave) as though all optional complexity is accidental. More than this, there is a strong bias in the Unix tradition toward removing features rather than accepting optional complexity.

The case for this attitude is easy to make (indeed, we spend much of this book making it). Clean minimalism makes us feel virtuous on many levels, and designing for it is a valuable counter to the natural tendency of software systems to develop ever-more-elaborate encrustations of ill-considered features. But computing resources and human thinking time, like wealth, find their justification not in being hoarded but in being spent. As with other forms of asceticism, one has to ask when design minimalism stops being a valuable form of self-discipline and starts being a mere hair shirt --- a way to indulge those feelings of virtue at the expense of actually [*using*]{.emphasis} that wealth to get work done.

This is a perilous question, all too easily turned into an argument for abandoning good design discipline altogether. Unix old hands often shy away from it, fearing that failing to hold the hardest possible line against complexity and bloat will lead us inexorably to damnation. But it\'s also a [*necessary*]{.emphasis} question. We\'ll tackle it directly when analyzing this chapter\'s case studies.
:::::

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[114](ch13s01.html#id2964826){#ftn.id2964826}\]^ The terms we have invented for these design traps, unlikely as they may sound, come from established hacker jargon described in \[[Raymond96](http://www.catb.org/~esr/writings/taoup/html/apb.html#Raymond96 "[Raymond96]")\].
:::

::: footnote
^\[[115](ch13s01.html#id2961828){#ftn.id2961828}\]^ The distinction between accidental and optional complexity means that the categories we\'re discussing here are [*not*]{.emphasis} the same as essence and accident in Fred Brooks\'s essay *No Silver Bullet* \[[Brooks](http://www.catb.org/~esr/writings/taoup/html/apb.html#Brooks "[Brooks]")\], but they have common ancestry in philosophy.
:::
:::::
:::::::::::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  ------------------------------------------------ --------------------------------------------- --------------------------------------
  [Prev](complexitychapter.html){accesskey="p"}     [Up](complexitychapter.html){accesskey="u"}     [Next](ch13s02.html){accesskey="n"}
  Chapter 13. Complexity                                 [Home](index.html){accesskey="h"}                       A Tale of Five Editors
  ------------------------------------------------ --------------------------------------------- --------------------------------------
:::
