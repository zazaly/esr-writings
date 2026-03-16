::: navheader
  Designing Minilanguages                                           
  -------------------------------------- -------------------------- ------------------------------------------------
  [Prev](ch08s02.html){accesskey="p"}     Chapter 8. Minilanguages     [Next](generationchapter.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::::::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2936349}Designing Minilanguages {#designing-minilanguages .title style="clear: both"}

</div>
::::

When is designing a minilanguage appropriate? We\'ve observed that minilanguages offer a way to push problem specifications to a higher level, and seen how this operates in several case studies. The flip side of this observation is that a minilanguage is likely to be a good approach whenever the domain primitives in your application area are simple and stereotyped, but the ways in which users are likely to want to apply them are fluid and varying.

For some related ideas, find a description of the [Alternate Hard And Soft Layers](http://www.c2.com/cgi/wiki?AlternateHardAndSoftLayers){target="_top"} and [Scripted Components](http://www.doc.ic.ac.uk/~np2/patterns/scripting/scripting.html){target="_top"} design patterns.

An interesting survey of design styles and techniques in minilanguages is []{#id2936393 .indexterm} *Notable Design Patterns for Domain-Specific Languages* \[[Spinellis](http://www.catb.org/~esr/writings/taoup/html/apb.html#Spinellis "[Spinellis]")\].

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2936413}Choosing the Right Complexity Level {#choosing-the-right-complexity-level .title}

</div>
::::

The first important thing to bear in mind when designing a minilanguage is, as usual, to keep it as simple as possible. The taxonomy diagram we used to organize the case studies implies a hierarchy of complexity; you want to keep your design as far toward the left-hand edge as possible. If you can get away with designing a structured data file rather than a minilanguage that is going to modify external data when it\'s interpreted, by all means do so.

One very pragmatic reason to stick with structured data rather than a minilanguage is that in a networked world, embedded minilanguage facilities are subject to abuses that can be inconvenient or even dangerous. JavaScript[]{#id2936439 .indexterm} is a prime example in the 'inconvenient' category; its designers didn\'t anticipate that it would be used for pop-up advertisements so obnoxious as to create a demand for browser features that suppress JavaScript interpretation.

Microsoft Word[]{#id2936456 .indexterm} macro viruses show how this sort of thing can become actively dangerous, a security hole that costs billions of dollars in downtime and lost productivity annually. It is instructive to note that despite the existence of at least twenty million Unix users worldwide^\[[95](ch08s03.html#ftn.id2936473){#id2936473}\]^ there has never been any Unix equivalent of Windows\'s frequent macro-virus outbreaks. There are a number of reasons for this, including the fundamentally better security design of Unix; but at least one is the fact that Unix mail agents do [*not*]{.emphasis} default to executing live content in any document that the user views.^\[[96](ch08s03.html#ftn.id2936490){#id2936490}\]^

If there is any way that your application\'s users might end up running programs from untrusted sources, risky features of your application minilanguage might end up having to be suppressed. Languages like Java and JavaScript are explicitly *sandboxed*---that is, they have limited access to their environment not merely to simplify their design but to try to prevent potentially destructive operations by buggy or malicious code.

On the other hand, a lot of bad designs have been botched by designers who failed to face up to the fact that they really needed a minilanguage rather than a data-file format. Too often, language-like features get pasted on as an afterthought. The two most common symptoms of this problem are weak, ad-hoc control structures and poor or nonexistent facilities for declaring procedures.

It\'s risky to design minilanguages that are only accidentally Turing-complete. If you do this the odds are good that, sometime in the future, some clever fellow is going to think he needs to press your language into doing loops and conditionals for him. Because these are only available in an obfuscated way, he\'ll produce obfuscated code. The results may be serviceable in the short term, but are likely to be a nightmare for those who come after him.

Minilanguage design is both powerful and esthetically rewarding, but it\'s also full of similar traps. There are kinds of design in which it is appropriate to take the bottom-up approach of pasting together a bunch of low-level services and worrying about their organization after you have explored the problem domain for a while. One of the virtues of minilanguages is that they can help you get a good design out of bottom-up programming by allowing you to defer some top-down decisions into the control flow of programs in your minilanguage. But if you take a bottom-up approach to the minilanguage design [*itself*]{.emphasis}, you are likely to end up with an ugly syntax reflecting a weak language and a poorly-thought-out implementation.

There are many places in a minilanguage design where small choices make a large difference in the useability and ease of the tool:

::: blockquote
  ------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                            As a language designer, it is a good principle to consider the alternatives to giving an error message. When there is true ambiguity in the intent of the programmer an error message is appropriate, but in many cases the intent is clear, and making the language silently do the right thing is a great boon. A good example is C accommodating an extra comma at the end of an array initializer list, which makes both editing and machine generation of array initializers much easier. Anti-examples are the pickiness of various HTML readers, especially their habit of silently discarding parts of your document because of trivial nesting errors.    
  \--[ [Steve Johnson]{.author} []{#id2936592 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      
  ------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

On this issue, as elsewhere, there is no substitute for good taste and engineering judgment. If you\'re going to design a minilanguage, don\'t do it halfway. Declarative minilanguages should have a clear, consistent language-like syntax designed to be readable by humans. Imperative ones should add a full range of control structures adapted from language models you can expect your users to be familiar with. Think about the language [*as*]{.emphasis} a language; ask yourself esthetic questions like "Will this be comfortable to program in?" and even "Will it be pleasant to look at?" Here, as elsewhere in software design, David Gelernter\'s maxim is apt: beauty is the ultimate defense against complexity.
::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2936650}Extending and Embedding Languages {#extending-and-embedding-languages .title}

</div>
::::

One fundamentally important question is whether you can implement your minilanguage by extending or embedding an existing scripting language[]{#id2936662 .indexterm}. This is often the right way to go for an imperative minilanguage, but much less appropriate for a declarative one.

Sometimes it\'s possible to write your imperative language simply by coding service functions in an interpreted language, which we\'ll call the 'host' language for purposes of this discussion. Your minilanguage programs are then just scripts that load your service library and use the host language\'s control structures and other facilities as a framework. Every facility the host language supplies is one you don\'t have to write.

This is the easiest way to write a minilanguage. Old-school Lisp[]{#id2936690 .indexterm} programmers (including me) love this technique and use it heavily. It underlies the design of the *Emacs* editor, and has been rediscovered in the new-school scripting languages like Tcl[]{#id2936708 .indexterm}, Python[]{#id2936717 .indexterm}, and Perl[]{#id2936725 .indexterm}. There are drawbacks to it, however.

Your host language may be unable to interface to a code library that you need. Or, internally, its ontology of data types may be inadequate for the kind of computation you need to do. Or, after measuring the performance of a prototype, you discover that it\'s too slow. When any of these things happen, your solution is usually going to involve coding in C[]{#id2936745 .indexterm} (or C++[]{#id2936753 .indexterm}) and integrating the results into your minilanguage.

The option of extending a scripting language[]{#id2936768 .indexterm} with C code, or of embedding a scripting language in a C program, relies on the existence of scripting languages designed for it. You extend a scripting language by telling it to dynamically load a C library or module in such a way that the C entry points become visible as functions in the extended language. You embed a scripting language in a C program by sending commands to an instance of the interpreter and receiving the results back as values in C.

Both techniques also rely on the ability to move data between the type ontology of C and the type ontology of your scripting language. Some scripting languages are designed from the ground up to support this. One such is Tcl[]{#id2936793 .indexterm}, which we\'ll cover in [Chapter 14](languageschapter.html "Chapter 14. Languages"). Another is *Guile*, an open-source dialect of the Lisp[]{#id2936815 .indexterm} variant Scheme. *Guile* is shipped as a library and specifically designed to be embedded in C[]{#id2936832 .indexterm} programs.

It is possible (though in 2003 still rather painful and difficult) to extend or embed Perl[]{#id2936846 .indexterm}. It is very easy to extend Python[]{#id2936854 .indexterm} and only slightly more difficult to embed it; C extension is especially heavily used in the Python world. Java[]{#id2936865 .indexterm} has an interface to call 'native methods' in C, though the practice is explicitly discouraged because it tends to break portability. Most versions of shell are not designed for embeddability and extension, but the Korn shell (ksh93 and later versions) is a notable exception.

There are lots of bad reasons not to piggyback your imperative minilanguage on an existing scripting language[]{#id2936885 .indexterm}. One of the few good ones is that you actually want to implement your own custom grammar for error checking. If that\'s the case, then see the advice about *yacc* and *lex* below.
:::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2936912}Writing a Custom Grammar {#writing-a-custom-grammar .title}

</div>
::::

For declarative minilanguages, one major question is whether or not you should use XML as a base syntax and specify your grammar as an XML document type. This may well be the right thing for elaborately structured declarative minilanguages, but the same caveats we noted in [Chapter 5](textualitychapter.html "Chapter 5. Textuality") about the design of data-file formats apply --- XML might be overkill. If you don\'t use XML, follow the Rule of Least Surprise by supporting the Unix conventions we described for data files (simple token-oriented syntax, supporting C[]{#id2936939 .indexterm} backslash conventions, etc.).

If you do need a custom grammar, *yacc* and *lex* (or their local equivalent in the language you\'re using) should probably be your best friends, unless the grammar of your language is so simple that hand-coding a recursive-descent parser is trivial. Even then, *yacc* may give you better error recovery, and a *yacc* specification will be easier to modify as the language syntax evolves. See [Chapter 9](generationchapter.html "Chapter 9. Generation") for a look at the *yacc*- and *lex*-derived tools available in different implementation languages.

Even if you decide you must implement your own syntax, consider what mileage you can get from reusing existing tools. If you need a macro facility, consider whether preprocessing with m4(1) might be the right answer --- but consider the cautions in the next section first.
:::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#macroexpansion}Macros --- Beware! {#macros-beware .title}

</div>
::::

Macro expansion facilities were a favored tactic for language designers in early Unix; the C[]{#id2937039 .indexterm} language has one, of course, and we have seen them show up in some of the more complex special-purpose minilanguages like pic(1). The *m4* preprocessor provides a generic tool for implementing macro-expanding preprocessors.

Macro expansion is easy to specify and implement, and you can do a lot of cute tricks with it. Those early designers appear to have been influenced by experience with assemblers, in which macro facilities were often the only device available for structuring programs.

The strength of macro expansion is that it knows nothing about the underlying syntax of the base language, and can be used to extend that syntax. Unfortunately, this power is very easily abused to produce code that is opaque, surprising, and a fertile source of hard-to-characterize bugs.

In C, the classic example of this sort of problem is a macro such as this:

``` programlisting
#define max(x, y)   x > y ? x : y
```

There are at least two problems with this macro. One is that it can produce surprising results if either of the arguments is an expression including an operator of lower precedence than `>` or `?:`. Consider the expression `max(a = b, ++c)`. If the programmer has forgotten that `max` is a macro, he will be expecting the assignment `a = b` and the preincrement operation on `c` to be executed before the resulting values are passed as arguments to `max`.

But that\'s not what will happen. Instead, the preprocessor will expand this expression to `a = b > ++c ? a = b : ++c`, which the C compiler\'s precedence rules make it interpret as `a = (b > ++c ? a = b : ++c)`. The effect will be to assign to `a`!

This sort of bad interaction can be headed off by coding the macro definition more defensively.

``` programlisting
#define max(x, y)   ((x) > (y) ? (x) : (y))
```

With this definition, the expansion would be `((a = b) > (++c) ? (a = b) : (++c))`. This solves one problem --- but notice that `c` may be incremented twice! There are subtler versions of this trap, such as passing the macro a function-call with side effects.

In general, interactions between macros and expressions with side effects can lead to unfortunate results that are hard to diagnose. C\'s macro processor is a deliberately lightweight and simple one; more powerful ones can actually get you in worse trouble.

The *TeX* formatting language (see [Chapter 18](http://www.catb.org/~esr/writings/taoup/html/documentationchapter.html "Chapter 18. Documentation")) well illustrates the general problem. *TeX* is intentionally Turing-complete (it has conditionals, loops, and recursion), but while it can be made to do amazing things, *TeX* code tends to be unreadable and painful to debug. The sources for *LaTeX*, the the most widely used *TeX* macro package, are an instructive example: they\'re in very good *TeX* style, but even so are extremely difficult to follow.

A minor problem, compared to this one, is that macro expansion tends to screw up error diagnostics. The base language processor generates its error reports relative to the macro expanded text, not the original the programmer is looking at. If the relationship between the two has been obfuscated by macro expansion, the emitted diagnostic can be very difficult to associate with the actual location of the error.

This is especially a problem with preprocessors and macros that can have multiline expansions, conditionally include or exclude text, or otherwise change line numbers in the expanded text.

Macro expansion stages that are built into a language can do their own compensation, fiddling line numbers to refer back to the preexpanded text. The macro facility in pic(1) does this, for example. This problem is more difficult to solve when the macro expansion is done by a preprocessor.

The C preprocessor[]{#id2937381 .indexterm} addresses this problem by emitting `#line` directives whenever it does an inclusion or multiline expansion. The C compiler is expected to interpret these and adjust the line numbers in its error reports accordingly. Unfortunately, *m4* has no such facility.

These are reasons to use macro expansion with extreme caution. One of the long-term lessons of the Unix experience is that macros tend to create more problems than they solve. Modern language and minilanguage designs have moved away from them.
:::::

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2937424}Language or Application Protocol? {#language-or-application-protocol .title}

</div>
::::

Another important question you need to ask is whether your minilanguage engine will be called interactively by other programs, as a slave process. If so, your design should probably look less like a conversational language for human interaction and more like the kind of application protocols we looked at in [Chapter 5](textualitychapter.html "Chapter 5. Textuality").

The main difference is how carefully marked the boundaries of transactions are. Human beings are good at spotting where conversational output from a CLI ends, and where the prompt for the next input is. They can use context to tell what\'s significant and what should be ignored. Computer programs have much more trouble with this. Without either unambiguous end markers on output or advance knowledge of the length of the output, they can\'t tell when to stop reading.

::: blockquote
  ----------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                          Even worse is when a program\'s input is buffered (often inadvertently, as by stdio). A program that stops overtly reading at the right place can nonetheless eat past it.    
  \--[[Doug McIlroy]{.author} []{#id2937475 .indexterm} ]{.attribution}                                                                                                                                                                                 
  ----------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Programs in which master processes are trying to do interactive things with slaved minilanguages that are not carefully designed around this problem are prone to deadlock as the master and slave fall out of synchronization (a problem we first noted in [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming")).

There are workarounds for driving minilanguages that are not so carefully designed. The prototype for most of them is the Tcl[]{#id2937516 .indexterm} *expect* package. This package assists conversation with CLIs. It\'s built around the following operation: read from slave until either a given regular-expression pattern is matched or a specified timeout elapses. With this (and, of course, a send-to-slave operation) it\'s often possible to construct master programs to do reliable dialogues with slave processes even when the latter have not been tailored for the role.

Workalikes of the *expect* package in other languages are available; a Web search for the name of your favorite language with the added keywords "Tcl expect" is quite likely to turn up something useful. As a minilanguage designer, however, you would be unwise to assume that all your users will be *expect* gurus. Even if they are, this is an extra glue layer and a place for things to go wrong.

Be aware of this issue when designing your minilanguage. It may be a good idea to add an option that changes its conversational behavior to make it respond more like an application protocol, with unambiguous end-of-output delimiters and an analog of [byte stuffing](ch05s04.html#byte_stuffing).
::::::

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[95](ch08s03.html#id2936473){#ftn.id2936473}\]^ 20M is a conservative estimate based on mid-2003 figures from the Linux Counter and elsewhere.
:::

::: footnote
^\[[96](ch08s03.html#id2936490){#ftn.id2936490}\]^ *Kmail*, which we looked at in [Chapter 6](transparencychapter.html "Chapter 6. Transparency"), won\'t even chase off-site links in HTML for this reason.
:::
:::::
:::::::::::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ------------------------------------------------ ------------------------------------------------
  [Prev](ch08s02.html){accesskey="p"}     [Up](minilanguageschapter.html){accesskey="u"}     [Next](generationchapter.html){accesskey="n"}
  Applying Minilanguages                        [Home](index.html){accesskey="h"}                                    Chapter 9. Generation
  -------------------------------------- ------------------------------------------------ ------------------------------------------------
:::
