::: navheader
  Nonlocality Considered Harmful                                    
  -------------------------------------- -------------------------- --------------------------------------
  [Prev](ch12s02.html){accesskey="p"}     Chapter 12. Optimization     [Next](ch12s04.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2961094}Nonlocality Considered Harmful {#nonlocality-considered-harmful .title style="clear: both"}

</div>
::::

The most effective way to optimize your code is to keep it small and simple. We\'ve been through lots of good reasons to keep it small and simple earlier in this book. Here\'s a new one: you want the central data structures and the time-critical loops in your code never to fall out of cache.

Consider your target machine as a hierarchy of memory types arranged by distance from the processor. There are the processor\'s own registers; its instruction pipeline; the level-one (L1) cache; the level-two (L2) cache; possibly a level-three (L3) cache; main memory (what Unix old hands still quaintly call 'core'); and the disk drives where swap space lives. Technologies like SMP, shared-memory clusters, and non-uniform memory access (NUMA) add more layers to the picture but only widen the overall spread.

Every kind of access to that stack is getting faster. Processor cycles are almost free, outside of a few demanding applications like modeling nuclear explosions or real-time video compression. But what\'s also happening is that the speed ratios between layers in the storage hierarchy are all increasing as processor speeds go up. Thus, the relative cost of a cache miss is increasing.

So we have an interesting paradox. As machine resources plummet, the expected cost of large data structures falls --- but because the cost spread between adjacent cache levels is also going up, the performance impact of being just large enough to break a cache boundary is also rising.

"Small is beautiful" is therefore better advice than ever, particularly with regard to central data structures that must live in the fastest possible cache. The advice applies to code as well; the average instruction spends more time being loaded than it does executing.

This turns some traditional advice on its head. Compiler optimizations like loop unrolling, which get rid of relatively expensive machine instructions in return for an increase in total code size, may no longer be worth doing. Another example is precomputing small tables --- for example, a table of sin(x) by degree for optimizing rotations in a 3D graphics engine will take 365 × 4 bytes on a modern machine. Before processors got enough faster than memory to demand caching, this was an obvious speed optimization. Nowadays it may be faster to recompute each time rather than pay for the percentage of additional cache misses caused by the table.

But in the future, this might turn around again as caches grow larger. More generally, many optimizations are temporary and can easily turn into pessimizations as cost ratios change. The only way to know is to measure and see.
:::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------------------- --------------------------------------
  [Prev](ch12s02.html){accesskey="p"}     [Up](optimizationchapter.html){accesskey="u"}     [Next](ch12s04.html){accesskey="n"}
  Measure before Optimizing                     [Home](index.html){accesskey="h"}                        Throughput vs. Latency
  -------------------------------------- ----------------------------------------------- --------------------------------------
:::
