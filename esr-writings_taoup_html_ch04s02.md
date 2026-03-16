::: navheader
  Compactness and Orthogonality                                  
  -------------------------------------- ----------------------- --------------------------------------
  [Prev](ch04s01.html){accesskey="p"}     Chapter 4. Modularity     [Next](ch04s03.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::::::::::::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2894547}Compactness and Orthogonality {#compactness-and-orthogonality .title style="clear: both"}

</div>
::::

Code is not the only sort of thing with an optimal chunk size. Languages and APIs (such as sets of library or system calls) run up against the same sorts of human cognitive constraints that produce Hatton\'s U-curve.

Accordingly, Unix programmers have learned to think very hard about two other properties when designing APIs, command sets, protocols, and other ways to make computers do tricks: *compactness* and *orthogonality*.

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#compactness}Compactness {#compactness .title}

</div>
::::

[]{#id2894585 .indexterm}

Compactness[]{#id2894599 .indexterm} is the property that a design can fit inside a human being\'s head. A good practical test for compactness is this: Does an experienced user normally need a manual? If not, then the design (or at least the subset of it that covers normal use) is compact.

Compact software tools have all the virtues of physical tools that fit well in the hand. They feel pleasant to use, they don\'t obtrude themselves between your mind and your work, they make you more productive --- and they are much less likely than unwieldy tools to turn in your hand and injure you.

Compact is not equivalent to 'weak'. A design can have a great deal of power and flexibility and still be compact if it is built on abstractions that are easy to think about and fit together well. Nor is compact equivalent to 'easily learned'; some compact designs are quite difficult to understand until you have mastered an underlying conceptual model that is tricky, at which point your view of the world changes and compact [*becomes*]{.emphasis} simple. For a lot of people, the Lisp language is a classic example of this[]{#id2894640 .indexterm}.

::: blockquote
  ---------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                         Nor does compact mean 'small'. If a well-designed system is predictable and 'obvious' to the experienced user, it might have quite a few pieces.    
  \--[ [Ken Arnold]{.author} []{#id2894663 .indexterm} ]{.attribution}                                                                                                                                                       
  ---------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Very few software designs are compact in an absolute sense, but many are compact in a slightly looser sense of the term. They have a compact working set, a subset of capabilities that suffices for 80% or more of what expert users normally do with them. Practically speaking, such designs normally need a reference card or cheat sheet but not a manual. We\'ll call such designs *semi-compact*, as opposed to *strictly compact*.

The concept is perhaps best illustrated by examples. The Unix system call API is semi-compact, but the standard C[]{#id2894706 .indexterm} library is not compact in any sense. While Unix programmers easily keep a subset of the system calls sufficient for most applications programming (file system operations, signals, and process control) in their heads, the C library on modern Unixes includes many hundreds of entry points, e.g., mathematical functions, that won\'t all fit inside a single programmer\'s cranium.

*The Magical Number Seven, Plus or Minus Two: Some Limits on Our Capacity for Processing Information* \[[Miller](http://www.catb.org/~esr/writings/taoup/html/apb.html#Miller "[Miller]")\] is one of the foundation papers in cognitive psychology (and, incidentally, the specific reason that U.S. local telephone numbers have seven digits). It showed that the number of discrete items of information human beings can hold in short-term memory is seven, plus or minus two. This gives us a good rule of thumb for evaluating the compactness of APIs: Does a programmer have to remember more than seven entry points? Anything larger than this is unlikely to be strictly compact.

Among Unix tools, make(1) is compact; autoconf(1) and automake(1) are not. Among markup languages, HTML is semi-compact, but DocBook (a documentation markup language we shall discuss in [Chapter 18](http://www.catb.org/~esr/writings/taoup/html/documentationchapter.html "Chapter 18. Documentation")) is not. The man(7) macros are compact, but troff(1) markup is not.

Among general-purpose programming languages, C[]{#id2894804 .indexterm} and Python[]{#id2894816 .indexterm} are semi-compact; Perl[]{#id2894824 .indexterm}, Java[]{#id2894832 .indexterm}, Emacs Lisp[]{#id2894841 .indexterm}, and shell[]{#id2894850 .indexterm} are not (especially since serious shell programming requires you to know half-a-dozen other tools like sed(1) and awk(1)). C++[]{#id2894877 .indexterm} is anti-compact --- the language\'s designer has admitted that he doesn\'t expect any one programmer to ever understand it all.

Some designs that are not compact have enough internal redundancy of features that individual programmers end up carving out compact dialects sufficient for that 80% of common tasks by choosing a working subset of the language. Perl has this kind of pseudo-compactness, for example. Such designs have a built-in trap; when two programmers try to communicate about a project, they may find that differences in their working subsets are a significant barrier to understanding and modifying the code.

Noncompact designs are not automatically doomed or bad, however. Some problem domains are simply too complex for a compact design to span them. Sometimes it\'s necessary to trade away compactness for some other virtue, like raw power and range. Troff markup is a good example of this. So is the BSD[]{#id2894911 .indexterm} sockets API. The purpose of emphasizing compactness as a virtue is not to condition you to treat compactness as an absolute requirement, but to teach you to do what Unix programmers do: value compactness properly, design for it whenever possible, and not throw it away casually.
::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#orthogonality}Orthogonality {#orthogonality .title}

</div>
::::

[]{#id2894936 .indexterm}

Orthogonality[]{#id2894950 .indexterm} is one of the most important properties that can help make even complex designs compact[]{#id2894960 .indexterm}. In a purely orthogonal design, operations do not have side effects; each action (whether it\'s an API call, a macro invocation, or a language operation) changes just one thing without affecting others. There is one and only one way to change each property of whatever system you are controlling.

Your monitor has orthogonal controls. You can change the brightness independently of the contrast level, and (if the monitor has one) the color balance control will be independent of both. Imagine how much more difficult it would be to adjust a monitor on which the brightness knob affected the color balance: you\'d have to compensate by tweaking the color balance every time after you changed the brightness. Worse, imagine if the contrast control also affected the color balance; then, you\'d have to adjust both knobs simultaneously in exactly the right way to change either contrast or color balance alone while holding the other constant.

Far too many software designs are non-orthogonal. One common class of design mistake, for example, occurs in code that reads and parses data from one (source) format to another (target) format. A designer who thinks of the source format as always being stored in a disk file may write the conversion function to open and read from a named file. Usually the input could just as well have been any file handle. If the conversion routine were designed orthogonally, e.g., without the side effect of opening a file, it could save work later when the conversion has to be done on a data stream supplied from standard input, a network socket, or any other source.

Doug McIlroy\'s[]{#id2895012 .indexterm} advice to "Do one thing well" is usually interpreted as being about simplicity. But it\'s also, implicitly and at least as importantly, about orthogonality.

It\'s not a problem for a program to do one thing well and other things as side effects, provided supporting those other things doesn\'t raise the complexity of the program and its vulnerability to bugs. In [Chapter 9](generationchapter.html "Chapter 9. Generation") we\'ll examine a program called *ascii* that prints synonyms for the names of ASCII characters, including hex, octal, and binary values; as a side effect, it can serve as a quick base converter for numbers in the range 0--255. This second use is not an orthogonality violation because the features that support it are all necessary to the primary function; they do not make the program more difficult to document or maintain.

The problems with non-orthogonality arise when side effects complicate a programmer\'s or user\'s mental model, and beg to be forgotten, with results ranging from inconvenient to dire. Even when you do not forget the side effects, you\'re often forced to do extra work to suppress them or work around them.

There is an excellent discussion of orthogonality and how to achieve it in *The Pragmatic Programmer* \[[Hunt-Thomas](http://www.catb.org/~esr/writings/taoup/html/apb.html#Hunt-Thomas "[Hunt-Thomas]")\]. As they point out, orthogonality reduces test and development time, because it\'s easier to verify code that neither causes side effects nor depends on side effects from other code --- there are fewer combinations to test. If it breaks, orthogonal code is more easily replaced without disturbance to the rest of the system. Finally, orthogonal code is easier to document and reuse.

The concept of *refactoring*, which first emerged as an explicit idea from the 'Extreme Programming' school, is closely related to orthogonality. To refactor code is to change its structure and organization without changing its observable behavior. Software engineers have been doing this since the birth of the field, of course, but naming the practice and identifying a stock set of refactoring techniques has helped concentrate peoples\' thinking in useful ways. Because these fit so well with the central concerns of the Unix design tradition, Unix developers have quickly coopted the terminology and ideas of refactoring.^\[[43](ch04s02.html#ftn.id2895110){#id2895110}\]^

The basic Unix APIs were designed for orthogonality with imperfect but considerable success. We take for granted being able to open a file for write access without exclusive-locking it for write, for example; not all operating systems are so graceful. Old-style (System III[]{#id2895143 .indexterm}) signals were non-orthogonal, because signal receipt had the side-effect of resetting the signal handler to the default die-on-receipt. There are large non-orthogonal patches like the BSD sockets[]{#id2895155 .indexterm} API and [*very*]{.emphasis} large ones like the X windowing system\'s drawing libraries.

But on the whole the Unix API is a good example: Otherwise it not only would not but [*could*]{.emphasis} not be so widely imitated by C[]{#id2895179 .indexterm} libraries on other operating systems. This is also a reason that the Unix API repays study even if you are not a Unix programmer; it has lessons about orthogonality to teach.
:::::

::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#spot_rule}The SPOT Rule {#the-spot-rule .title}

</div>
::::

[]{#id2895202 .indexterm}

*The Pragmatic Programmer* articulates a rule for one particular kind of orthogonality that is especially important. Their "Don\'t Repeat Yourself" rule is: every piece of knowledge must have a [*single*]{.emphasis}, unambiguous, authoritative representation within a system. In this book we prefer, following a suggestion by Brian Kernighan, to call this the Single Point Of Truth or SPOT rule.

Repetition leads to inconsistency and code that is subtly broken, because you changed only some repetitions when you needed to change [*all*]{.emphasis} of them. Often, it also means that you haven\'t properly thought through the organization of your code.

Constants, tables, and metadata should be declared and initialized [*once*]{.emphasis} and imported elsewhere. Any time you see duplicate code, that\'s a danger sign. Complexity is a cost; don\'t pay it twice.

Often it\'s possible to remove code duplication by *refactoring*; that is, changing the organization of your code without changing the core algorithms. Data duplication sometimes appears to be forced on you. But when you see it, here are some valuable questions to ask:

::: itemizedlist
-   If you have duplicated data in your code because it has to have two different representations in two different places, can you write a function, tool or code generator to make one representation from the other, or both from a common source?

-   If your documentation duplicates knowledge in your code, can you generate parts of the documentation from parts of the code, or vice-versa, or both from a common higher-level representation?

-   If your header files and interface declarations duplicate knowledge in your implementation code, is there a way you can generate the header files and interface declarations from the code?
:::

There is an analog of the SPOT rule for data structures: "No junk, no confusion". "No junk" says that the data structure (the model) should be minimal, e.g., not made so general that it can represent situations which cannot exist. "No confusion" says that states which must be kept distinct in the real-world problem must be kept distinct in the model. In short, the SPOT rule advocates seeking a data structure whose states have a one-to-one correspondence with the states of the real-world system to be modeled.

From deeper within the Unix tradition, we can add some of our own corollaries of the SPOT rule:

::: itemizedlist
-   Are you duplicating data because you\'re caching intermediate results of some computation or lookup? Consider carefully whether this is premature optimization[]{#id2895355 .indexterm}; stale caches (and the layers of code needed to keep caches synchronized) are a fertile source of bugs,^\[[44](ch04s02.html#ftn.id2895368){#id2895368}\]^ and can even slow down overall performance if (as often happens) the cache-management overhead is higher than you expected.

-   If you see lots of duplicative boilerplate code, can you generate all of it from a single higher-level representation, twiddling a few knobs to generate the different cases?
:::

The reader should begin to see a pattern emerging here.

In the Unix world, the SPOT Rule as a unifying idea has seldom been explicit --- but heavy use of code generators to implement particular [*kinds*]{.emphasis} of SPOT are very much part of the tradition. We\'ll survey these techniques in [Chapter 9](generationchapter.html "Chapter 9. Generation").
:::::::

:::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2895445}Compactness and the Strong Single Center {#compactness-and-the-strong-single-center .title}

</div>
::::

One subtle but powerful way to promote compactness in a design is to organize it around a strong core algorithm addressing a clear formal definition of the problem, avoiding heuristics and fudging.

::: blockquote
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                           Formalization often clarifies a task spectacularly. It is not enough for a programmer to recognize that bits of his task fall within standard computer-science categories --- a little depth-first search here and a quicksort there. The best results occur when the nub of the task can be formalized, and a clear model of the job at hand can be constructed. It is not necessary that ultimate users comprehend the model. The very existence of a unifying core will provide a comfortable feel, unencumbered with the why-in-hell-did-they-do-that moments that are so prevalent in using Swiss-army-knife programs.    
  \--[ [Doug McIlroy]{.author} []{#id2895473 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

This is an often-overlooked strength of the Unix tradition. Many of its most effective tools are thin wrappers around a direct translation of some single powerful algorithm.

Perhaps the clearest example of this is diff(1), the Unix tool for reporting differences between related files. This tool and its dual, patch(1), have become central to the network-distributed development style of modern Unix. A valuable property of diff is that it seldom surprises anyone. It doesn\'t have special cases or painful edge conditions, because it uses a simple, mathematically sound method of sequence comparison. This has consequences:

::: blockquote
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                           By virtue of a mathematical model and a solid algorithm, Unix diff contrasts markedly with its imitators. First, the central engine is solid, small, and has never needed one line of maintenance. Second, the results are clear and consistent, unmarred by surprises where heuristics fail.    
  \--[ [Doug McIlroy]{.author} []{#id2895550 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                    
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Thus, people who use diff can develop an intuitive feel for what it will do in any given situation without necessarily understanding the central algorithm perfectly. Other well-known examples of this special kind of clarity achieved through a strong central algorithm abound in Unix:

::: itemizedlist
-   The grep(1) utility for selecting lines out of files by pattern matching is a simple wrapper around a formal algebra of regular-expression patterns (see [the section called "Case Study: Regular Expressions"](ch08s02.html#regexps "Case Study: Regular Expressions") for discussion). If it had lacked this consistent mathematical model, it would probably look like the design of the original glob(1) facility in the oldest Unixes, a handful of ad-hoc wildcards that can\'t be combined.

-   The yacc(1) utility for generating language parsers is a thin wrapper around the formal theory of LR(1) grammars. Its partner, the lexical analyzer generator lex(1), is a similarly thin wrapper around the theory of nondeterministic finite-state automata.
:::

All three of these programs are so bug-free that their correct functioning is taken utterly for granted, and compact enough to fit easily in a programmer\'s hand. Only a part of these good qualities are due to the polishing that comes with a long service life and frequent use; most of it is that, having been constructed around a strong and provably correct algorithmic core, they never needed much polishing in the first place.

The opposite of a formal approach is using *heuristics*---rules of thumb leading toward a solution that is probabilistically, but not certainly, correct. Sometimes we use heuristics because a deterministically correct solution is impossible. Think of spam filtering, for example; an algorithmically perfect spam filter would need a full solution to the problem of understanding natural language as a module. Other times, we use heuristics because known formally correct methods are impossibly expensive. Virtual-memory management is an example of this; there are near-perfect solutions, but they require so much runtime instrumentation that their overhead would swamp any theoretical gain over heuristics.

The trouble with heuristics is that they proliferate special cases and edge cases. If nothing else, you usually have to backstop a heuristic with some sort of recovery mechanism when it fails. All the usual problems with escalating complexity follow. To manage the resulting tradeoffs, you have to start by being aware of them. Always ask if a heuristic actually pays off in performance what it costs in code complexity --- and don\'t guess at the performance difference, actually measure it before making a decision.
::::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2899405}The Value of Detachment {#the-value-of-detachment .title}

</div>
::::

We began this book with a reference to Zen: "a special transmission, outside the scriptures". This was not mere exoticism for stylistic effect; the core concepts of Unix have always had a spare, Zen-like simplicity that continues to shine through the layers of historical accidents that have accreted around them[]{#id2899424 .indexterm}. This quality is reflected in the cornerstone documents of Unix, like *The C Programming Language* \[[Kernighan-Ritchie](http://www.catb.org/~esr/writings/taoup/html/apb.html#Kernighan-Ritchie "[Kernighan-Ritchie]")\] and the 1974 CACM paper that introduced Unix to the world; one of the famous quotes from that paper observes "\...constraint has encouraged not only economy, but also a certain elegance of design". That simplicity came from trying to think not about how much a language or operating system could do, but of how [*little*]{.emphasis} it could do --- not by carrying assumptions but by starting from zero (what in Zen is called "beginner\'s mind" or "empty mind").

To design for compactness[]{#id2899472 .indexterm} and orthogonality[]{#id2899480 .indexterm}, start from zero. Zen teaches that attachment leads to suffering; experience with software design teaches that attachment to unnoticed assumptions leads to non-orthogonality, noncompact designs, and projects that fail or become maintenance nightmares.

To achieve enlightenment and surcease from suffering, Zen teaches detachment. The Unix tradition teaches the value of detachment from the particular, accidental conditions under which a design problem was posed. Abstract. Simplify. Generalize. Because we write software to solve problems, we cannot completely detach from the problems --- but it is well worth the mental effort to see how many preconceptions you can throw away, and whether the design becomes more compact[]{#id2899507 .indexterm} and orthogonal as you do that. Possibilities for code reuse often result.

Jokes about the relationship between Unix and Zen are a live part of the Unix tradition as well.^\[[45](ch04s02.html#ftn.id2899522){#id2899522}\]^ This is not an accident.
:::::

:::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[43](ch04s02.html#id2895110){#ftn.id2895110}\]^ In the foundation text on this topic, *Refactoring* \[[Fowler](http://www.catb.org/~esr/writings/taoup/html/apb.html#Fowler "[Fowler]")\], the author comes very close to stating that the principal goal of refactoring is to improve orthogonality. But lacking the concept, he can only approximate this idea from several different directions: eliminating code duplication and various other "bad smells" many of which are some sort of orthogonality violation.
:::

::: footnote
^\[[44](ch04s02.html#id2895368){#ftn.id2895368}\]^ An archetypal example of bad caching is the **rehash** directive in csh(1); type **man 1 csh** for details. See [the section called "Caching Operation Results"](ch12s04.html#binary_caches "Caching Operation Results") for another example.
:::

::: footnote
^\[[45](ch04s02.html#id2899522){#ftn.id2899522}\]^ For a recent example of Unix/Zen crossover, see [Appendix D](http://www.catb.org/~esr/writings/taoup/html/unix_koans.html "Appendix D. Rootless Root").
:::
::::::
::::::::::::::::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  ---------------------------------------- --------------------------------------------- --------------------------------------
  [Prev](ch04s01.html){accesskey="p"}       [Up](modularitychapter.html){accesskey="u"}     [Next](ch04s03.html){accesskey="n"}
  Encapsulation and Optimal Module Size          [Home](index.html){accesskey="h"}             Software Is a Many-Layered Thing
  ---------------------------------------- --------------------------------------------- --------------------------------------
:::
