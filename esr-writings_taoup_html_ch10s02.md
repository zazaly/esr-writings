::: navheader
  Where Configurations Live                                          
  -------------------------------------- --------------------------- --------------------------------------
  [Prev](ch10s01.html){accesskey="p"}     Chapter 10. Configuration     [Next](ch10s03.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2941727}Where Configurations Live {#where-configurations-live .title style="clear: both"}

</div>
::::

Classically, a Unix program can look for control information in five places in its startup-time environment:

::: itemizedlist
-   Run-control files under `/etc` (or at fixed location elsewhere in systemland).

-   System-set environment variables.

-   Run-control files (or 'dotfiles') in the user\'s home directory. (See [Chapter 3](contrastchapter.html "Chapter 3. Contrasts") for a discussion of this important concept, if it is unfamiliar.)

-   User-set environment variables.

-   Switches and arguments passed to the program on the command line that invoked it.
:::

These queries are usually done in the order listed above. That way, later (more local) settings override earlier (more global) ones. Settings found earlier can help the program compute locations for later retrievals of configuration data.

When thinking about which mechanism to use to pass configuration data to a program, bear in mind that good Unix practice demands using whichever one most closely matches the expected lifetime of the preference. Thus: for preferences which are very likely to change between invocations, use command-line switches. For preferences which change seldom, but that should be under individual user control, use a run-control file in the user\'s home directory. For preference information that needs to be set site-wide by a system administrator and [*not*]{.emphasis} changed by users, use a run-control file in system space.

We\'ll discuss each of these places in more detail, then examine some case studies.
::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ------------------------------------------------ --------------------------------------
  [Prev](ch10s01.html){accesskey="p"}     [Up](configurationchapter.html){accesskey="u"}     [Next](ch10s03.html){accesskey="n"}
  What Should Be Configurable?                  [Home](index.html){accesskey="h"}                              Run-Control Files
  -------------------------------------- ------------------------------------------------ --------------------------------------
:::
