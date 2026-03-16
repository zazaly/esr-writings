::: navheader
  The Right Size of Software                                      
  -------------------------------------- ------------------------ ---------------------------------------------
  [Prev](ch13s03.html){accesskey="p"}     Chapter 13. Complexity     [Next](implementation.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2968013}The Right Size of Software {#the-right-size-of-software .title style="clear: both"}

</div>
::::

There is a hidden dual of the Unix gospel of small, sharp tools; a background so implicit that many Unix practitioners do not notice it, any more than fish notice the water they swim in. It is the presence of frameworks.

Small, sharp tools in the Unix style have trouble sharing data, unless they live inside a framework that makes communication among them easy. Emacs is such a framework, and [*unified management of shared context*]{.emphasis} is what the optional complexity of Emacs is buying. The practical impact of unified management of shared context is that the user is not burdened with low-level naming and resource-management issues.

In old-school Unix, the only framework was pipelines, redirection, and the shell; the integration was done with scripts, and the shared context was (essentially) the file system itself. But that was not the end of evolution.

Emacs unifies the file system with a world of text buffers and helper processes, largely leaving the shell framework behind. Wily is also about buffers and helpers, but incorporates the shell framework into itself. Modern desktop environments provide a communication framework for GUIs, also leaving the shell framework behind. Each framework has strengths and weaknesses of its own. Frameworks become homes to ecologies of tools --- the shell to shellscripts, Emacs to Lisp modes, and desktop environments to flocks of GUIs communicating both via drag and drop and by more esoteric means such as object brokers.

This suggests a Rule of Minimality: [*Choose the shared context you want to manage, and build your programs as small as those boundaries will allow.*]{.emphasis} This is "as simple as possible, but no simpler", but it focuses attention on the choice of shared context. It applies not just to frameworks, but to applications and program systems.

It is, however, all too easy to get sloppy about how large your shared context needs to be. The pressure behind Zawinski\'s Law is the tendency of applications to want to share context for convenience. It\'s easy to end up carrying around too much weight, too many assumptions, and to write programs that are over-complex, bloated, and huge. The paradigmatic example in the 1990s was the way that the mailto: URL induced the growth of huge mail clients embedded in Web browsers.

The corrective to this tendency comes straight from the old-school Unix hymnbook. It is the Rule of Parsimony: [*Write a big program only when it is clear by demonstration that nothing else will do*]{.emphasis}---that is, when attempts to partition the problem have been made and failed. This maxim implies an astringent skepticism about large programs, and a strategy for avoiding them: look for the small-program solution first. If a single small program won\'t do the job, try building a toolkit of cooperating small programs within an existing framework to attack it. Only if both approaches fail are you free (in the Unix tradition) to build a large program (or a new framework) without feeling you have failed the design challenge.

When you do write a framework, remember the Rule of Separation. Frameworks should be mechanism, and have as little policy as possible. In most cases, that is no policy at all. Factor as much behavior as possible into modules that use the framework. One of the benefits of writing or reusing a framework is that it can help you separate what would otherwise be big lumps of policy into separate modules, modes, or tools --- pieces that can be usefully recombined with others.

These rules are valuable heuristics, but the tension at the heart of the Unix tradition does not resolve neatly into a set of [*a-priori*]{.foreignphrase} prescriptions for optimal size of any given project. Circumstances alter cases, and exercising good judgment and good taste is what software designers are for. As in Soto Zen, the journey [*is*]{.emphasis} the destination; enlightenment has to be rediscovered in every day of practice.
:::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- --------------------------------------------- ---------------------------------------------
  [Prev](ch13s03.html){accesskey="p"}     [Up](complexitychapter.html){accesskey="u"}     [Next](implementation.html){accesskey="n"}
  The Right Size for an Editor                 [Home](index.html){accesskey="h"}                            Part III. Implementation
  -------------------------------------- --------------------------------------------- ---------------------------------------------
:::
