::: navheader
  Applying the Rule of Least Surprise                                      
  ----------------------------------------------- ------------------------ --------------------------------------
  [Prev](interfacechapter.html){accesskey="p"}     Chapter 11. Interfaces     [Next](ch11s02.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2952650}Applying the Rule of Least Surprise {#applying-the-rule-of-least-surprise .title style="clear: both"}

</div>
::::

The Rule of Least Surprise is a general principle in the design of all kinds of interfaces, not just software: "Do the least surprising thing". It\'s a consequence of the fact that human beings can only pay attention to one thing at one time (see *The Humane Interface* \[[Raskin](http://www.catb.org/~esr/writings/taoup/html/apb.html#Raskin "[Raskin]")\]). Surprises in the interface focus that single locus of attention on the interface, rather than on the task where it belongs.

Thus, to design usable interfaces, it\'s best when possible not to design an entire new interface model. Novelty is a barrier to entry; it puts a learning burden on the user, so minimize it. Instead, think carefully about the experience and knowledge of your user base. Try to find functional similarities between your program and programs they are likely to already know about. Then mimic the relevant parts of the existing interfaces.

The Rule of Least Surprise should not be interpreted as a call for mechanical conservatism in design. Novelty raises the cost of a user\'s first few interactions with an interface, but poor design will make the interface needlessly painful forever. As in other sorts of design, rules are not a substitute for good taste and engineering judgment. Consider your tradeoffs carefully --- and consider them from the [*user\'s*]{.emphasis} point of view. The bias implied by the Rule of Least Surprise is a good one to hold consciously, mainly because interface designers (like other programmers) have an unconscious tendency to be too clever for the user\'s good.

One implication of the Rule of Least Surprise is this: Wherever possible, allow the user to delegate interface functions to a familiar program. We already observed in [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming") that, if your program requires the user to edit significant amounts of text, you should write it to call an editor (specifiable by the user) rather than building in your own integrated editor. This will enable the [*users*]{.emphasis}, who know their preferences better than you, to choose the least surprising alternative.

Elsewhere in this book we have advocated symbiosis and delegation as tactics for promoting code reuse and minimizing complexity. The point here is that when users can intercept the delegation, and direct it to an agent of their own choice, these techniques become not merely economical for the developer but actively empowering to users.

Further: When you can\'t delegate, emulate. The purpose of the Rule of Least Surprise is to reduce the amount of complexity a user must absorb to use an interface. Continuing the editor example, this means that if you must implement an embedded editor, it\'s best if the editor commands are a subset of those for a well-known general-purpose editor. (Or more than one. Both *bash* and *ksh* have command-line editors that allow the user to choose between *vi* and *Emacs* editing styles.)

Under the Unix versions of the Netscape and Mozilla Web browsers, for example, fill-in fields in forms recognize a subset of the default bindings for the *Emacs* editor. Control-A goes to start of line, Control-D deletes the next character, and so forth. This choice helps people who know *Emacs*, and leaves others no worse off than an arbitrary, idiosyncratic command set would have. The only way it could have been bettered was by choosing key bindings associated with some editor significantly more widely used than *Emacs*; and among Netscape\'s original user population there was no such animal.

These principles can be applied in many other areas of interface design. They suggest, for example, that it is deeply foolish to create novel document formats for an on-line help system when users are comfortable with an HTML Web browser. Or even that if you are designing an arcade-style game, it is wise to look at the gesture sets of previous games to see if you can give new users a feeling of comfort by allowing them to transfer joystick skills learned in other games.
:::::

::: navfooter

------------------------------------------------------------------------

  ----------------------------------------------- -------------------------------------------- --------------------------------------
  [Prev](interfacechapter.html){accesskey="p"}     [Up](interfacechapter.html){accesskey="u"}     [Next](ch11s02.html){accesskey="n"}
  Chapter 11. Interfaces                               [Home](index.html){accesskey="h"}          History of Interface Design on Unix
  ----------------------------------------------- -------------------------------------------- --------------------------------------
:::
