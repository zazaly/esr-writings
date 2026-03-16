::: navheader
  Chapter 10. Configuration                                
  -------------------------------------- ----------------- --------------------------------------
  [Prev](ch09s02.html){accesskey="p"}     Part II. Design     [Next](ch10s01.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::: {.chapter lang="en"}
::::: titlepage
<div>

## []{#configurationchapter}Chapter 10. Configuration {#chapter-10.-configuration .title}

</div>

<div>

### *Starting on the Right Foot* {#starting-on-the-right-foot .subtitle}

</div>
:::::

::: toc
**Table of Contents**

[What Should Be Configurable?](ch10s01.html)

[Where Configurations Live](ch10s02.html)

[Run-Control Files](ch10s03.html)

[Case Study: The .netrc File](ch10s03.html#id2942210)

[Portability to Other Operating Systems](ch10s03.html#id2942358)

[Environment Variables](ch10s04.html)

[System Environment Variables](ch10s04.html#id2942463)

[User Environment Variables](ch10s04.html#id2942749)

[When to Use Environment Variables](ch10s04.html#id2942882)

[Portability to Other Operating Systems](ch10s04.html#id2947980)

[Command-Line Options](ch10s05.html)

[The -a to -z of Command-Line Options](ch10s05.html#id2948149)

[Portability to Other Operating Systems](ch10s05.html#id2950162)

[How to Choose among the Methods](ch10s06.html)

[Case Study: fetchmail](ch10s06.html#fetchmail_environment)

[Case Study: The XFree86 Server](ch10s06.html#id2950578)

[On Breaking These Rules](ch10s07.html)
:::

::: {.epigraph xmlns=""}

Let us watch well our beginnings, and results will manage themselves.

\--*[ [Alexander Clark]{.author} ]{.attribution xmlns="http://www.w3.org/1999/xhtml"}*
:::

Under Unix, programs can communicate with their environment in a rich variety of ways. It\'s convenient to divide these into (a) startup-environment queries and (b) interactive channels. In this chapter, we\'ll focus primarily on startup-environment queries. The next chapter will discuss interactive channels.
::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------- --------------------------------------
  [Prev](ch09s02.html){accesskey="p"}     [Up](design.html){accesskey="u"}      [Next](ch10s01.html){accesskey="n"}
  Ad-hoc Code Generation                  [Home](index.html){accesskey="h"}            What Should Be Configurable?
  -------------------------------------- ----------------------------------- --------------------------------------
:::
