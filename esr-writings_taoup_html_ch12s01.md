::: navheader
  Don\'t Just Do Something, Stand There!                                        
  -------------------------------------------------- -------------------------- --------------------------------------
  [Prev](optimizationchapter.html){accesskey="p"}     Chapter 12. Optimization     [Next](ch12s02.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2962084}Don\'t Just Do Something, Stand There! {#dont-just-do-something-stand-there .title style="clear: both"}

</div>
::::

The most powerful optimization technique in any programmer\'s toolbox is to do nothing.

This very Zen advice is true for several reasons. One is the exponential effect of Moore\'s Law --- the smartest, cheapest, and often [*fastest*]{.emphasis} way to collect performance gains is to wait a few months for your target hardware to become more capable. Given the cost ratio between hardware and programmer time, there are almost always better things to do with your time than to optimize a working system.

We can get mathematically specific about this. It is almost never worth doing optimizations that reduce resource use by merely a constant factor; it\'s smarter to concentrate effort on cases in which you can reduce average-case running time or space use from O([*n*]{.emphasis}^2^) to O([*n*]{.emphasis}) or O([*n*]{.emphasis} log [*n*]{.emphasis}),^\[[112](ch12s01.html#ftn.id2962140){#id2962140}\]^ or similarly reduce from a higher order. Linear performance gains tend to be rapidly swamped by Moore\'s Law.^\[[113](ch12s01.html#ftn.id2960862){#id2960862}\]^

Another very constructive form of doing nothing is to not write code. The program can\'t be slowed down by code that isn\'t there. It can be slowed down by code that [*is*]{.emphasis} there but less efficient than it could be --- but that\'s a different matter.

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[112](ch12s01.html#id2962140){#ftn.id2962140}\]^ For readers unfamiliar with O notation, it is a way of indicating how the average running time of an algorithm changes with the size of its inputs. An O(1) algorithm runs in constant time. An O([*n*]{.emphasis}) algorithm runs in a time that is predicted by `A`[*`n`*]{.emphasis}` + C`, where `A` is some unknown constant of proportionality and `C` is an unknown constant representing setup time. Linear search of a list for a specified value is O([*n*]{.emphasis}). An O([*n*]{.emphasis}^2^) algorithm runs in time `A`[*`n`*]{.emphasis}^`2`^ plus lower-order terms (which might be linear, or logarithmic, of any other function lower than a quadratic). Checking a list for duplicate values (by the naïve method, not sorting it) is O([*n*]{.emphasis}^2^). Similarly, O([*n*]{.emphasis}^3^) algorithms have an average run time predicted by the cube of problem size; these tend to be too slow for practical use. O(log [*n*]{.emphasis}) is typical of tree searches. Intelligent choice of algorithm can often reduce running time from O([*n*]{.emphasis}^2^) to O(log [*n*]{.emphasis}). Sometimes when we are interested in predicting an algorithm\'s memory utilization, we may notice that it varies as O(1) or O([*n*]{.emphasis}) or O([*n*]{.emphasis}^2^); in general, algorithms with O([*n*]{.emphasis}^2^) or higher memory utilization are not practical either.
:::

::: footnote
^\[[113](ch12s01.html#id2960862){#ftn.id2960862}\]^ The eighteen-month doubling time usually quoted for Moore\'s Law implies that you can collect a 26% performance gain just by buying new hardware in six months.
:::
:::::
::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------------------- ----------------------------------------------- --------------------------------------
  [Prev](optimizationchapter.html){accesskey="p"}     [Up](optimizationchapter.html){accesskey="u"}     [Next](ch12s02.html){accesskey="n"}
  Chapter 12. Optimization                                  [Home](index.html){accesskey="h"}                     Measure before Optimizing
  -------------------------------------------------- ----------------------------------------------- --------------------------------------
:::
