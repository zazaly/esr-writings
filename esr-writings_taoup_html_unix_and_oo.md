::: navheader
  Unix and Object-Oriented Languages                             
  -------------------------------------- ----------------------- --------------------------------------
  [Prev](ch04s04.html){accesskey="p"}     Chapter 4. Modularity     [Next](ch04s06.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#unix_and_oo}Unix and Object-Oriented Languages {#unix-and-object-oriented-languages .title style="clear: both"}

</div>
::::

[]{#id2900532 .indexterm}

Since the mid-1980s most new language designs have included native support for *object-oriented programming* (OO). Recall that in object-oriented programming, the functions that act on a particular data structure are encapsulated with the data in an object that can be treated as a unit. By contrast, modules in non-OO languages make the association between data and the functions that act on it rather accidental, and modules frequently leak data or bits of their internals into each other.

The OO design concept initially proved valuable in the design of graphics systems, graphical user interfaces, and certain kinds of simulation. To the surprise and gradual disillusionment of many, it has proven difficult to demonstrate significant benefits of OO outside those areas. It\'s worth trying to understand why.

There is some tension and conflict between the Unix tradition of modularity and the usage patterns that have developed around OO languages. Unix programmers have always tended to be a bit more skeptical about OO than their counterparts elsewhere. Part of this is because of the Rule of Diversity; OO has far too often been promoted as the One True Solution to the software-complexity problem. But there is something else behind it as well, an issue which is worth exploring as background before we evaluate specific OO (object-oriented) languages in [Chapter 14](languageschapter.html "Chapter 14. Languages"). It will also help throw some characteristics of the Unix style of non-OO programming into sharper relief.

We observed above that the Unix tradition of modularity is one of thin glue, a minimalist approach with few layers of abstraction between the hardware and the top-level objects of a program. Part of this is the influence of C. It takes serious effort to simulate true objects in C. Because that\'s so, piling up abstraction layers is an exhausting thing to do. Thus, object hierarchies in C tend to be relatively flat and transparent[]{#id2900606 .indexterm}. Even when Unix programmers use other languages, they tend to want to carry over the thin-glue/shallow-layering style that Unix models have taught them.

OO languages make abstraction easy --- perhaps too easy. They encourage architectures with thick glue and elaborate layers. This can be good when the problem domain is truly complex and demands a lot of abstraction, but it can backfire badly if coders end up doing simple things in complex ways just because they can.

All OO languages show some tendency to suck programmers into the trap of excessive layering. Object frameworks and object browsers are not a substitute for good design or documentation, but they often get treated as one. Too many layers destroy transparency[]{#id2900640 .indexterm}: It becomes too difficult to see down through them and mentally model what the code is actually doing. The Rules of Simplicity, Clarity, and Transparency get violated wholesale, and the result is code full of obscure bugs and continuing maintenance problems.

This tendency is probably exacerbated because a lot of programming courses teach thick layering as a way to satisfy the Rule of Representation. In this view, having lots of classes is equated with embedding knowledge in your data. The problem with this is that too often, the 'smart data' in the glue layers is not actually about any natural entity in whatever the program is manipulating --- it\'s just about being glue. (One sure sign of this is a proliferation of abstract subclasses or 'mixins'.)

Another side effect of OO abstraction is that opportunities for optimization[]{#id2900675 .indexterm} tend to disappear. For example, [*a*]{.emphasis} + [*a*]{.emphasis} + [*a*]{.emphasis} + [*a*]{.emphasis} can become [*a*]{.emphasis} \* 4 and even [*a*]{.emphasis} \<\< 2 if a is an integer. But if one creates a class with operators, there is nothing to indicate if they are commutative, distributive, or associative. Since one isn\'t supposed to look inside the object, it\'s not possible to know which of two equivalent expressions is more efficient. This isn\'t in itself a good reason to avoid using OO techniques on new projects; that would be premature optimization[]{#id2900717 .indexterm}. But it is reason to think twice before transforming non-OO code into a class hierarchy.

Unix programmers tend to share an instinctive sense of these problems. This tendency appears to be one of the reasons that, under Unix, OO languages have failed to displace non-OO workhorses like C[]{#id2900738 .indexterm}, Perl[]{#id2900746 .indexterm} (which actually has OO facilities, but they\'re not heavily used), and shell[]{#id2900756 .indexterm}. There is more vocal criticism of OO in the Unix world than orthodoxy permits elsewhere; Unix programmers know when [*not*]{.emphasis} to use OO; and when they do use OO languages, they spend more effort on trying to keep their object designs uncluttered. As the author of *The Elements of Networking Style* once observed in a slightly different context \[[Padlipsky](http://www.catb.org/~esr/writings/taoup/html/apb.html#Padlipsky "[Padlipsky]")\]: "If you know what you\'re doing, three layers is enough; if you don\'t, even seventeen levels won\'t help".

One reason that OO has succeeded most where it has (GUIs, simulation, graphics) may be because it\'s relatively difficult to get the ontology of types wrong in those domains. In GUIs and graphics, for example, there is generally a rather natural mapping between manipulable visual objects and classes. If you find yourself proliferating classes that have no obvious mapping to what goes on in the display, it is correspondingly easy to notice that the glue has gotten too thick.

One of the central challenges of design in the Unix style is how to combine the virtue of detachment (simplifying and generalizing problems from their original context) with the virtue of thin glue and shallow, flat, transparent hierarchies of code and design[]{#id2900812 .indexterm}.

We\'ll return to some of these points and apply them when we discuss object-oriented languages in [Chapter 14](languageschapter.html "Chapter 14. Languages").
:::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- --------------------------------------------- --------------------------------------
  [Prev](ch04s04.html){accesskey="p"}     [Up](modularitychapter.html){accesskey="u"}     [Next](ch04s06.html){accesskey="n"}
  Libraries                                    [Home](index.html){accesskey="h"}                        Coding for Modularity
  -------------------------------------- --------------------------------------------- --------------------------------------
:::
