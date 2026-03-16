::: navheader
  Libraries                                                      
  -------------------------------------- ----------------------- ------------------------------------------
  [Prev](ch04s03.html){accesskey="p"}     Chapter 4. Modularity     [Next](unix_and_oo.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2900219}Libraries {#libraries .title style="clear: both"}

</div>
::::

One consequence of the emphasis that the Unix programming style put on modularity and well-defined APIs is a strong tendency to factor programs into bits of glue connecting collections of libraries, especially shared libraries (the equivalents of what are called dynamically-linked libraries or DLLs under Windows and other operating systems).

If you are careful and clever about design, it is often possible to partition a program so that it consists of a user-interface-handling main section (policy) and a collection of service routines (mechanism) with effectively no glue at all. This approach is especially appropriate when the program has to do a lot of very specific manipulations of data structures like graphic images, network-protocol packets, or control blocks for a hardware interface. Some good general architectural advice from within the Unix tradition, particularly applicable to the resource-management challenges of this sort of library is collected in *The Discipline and Method Architecture for Reusable Libraries* \[[Vo](http://www.catb.org/~esr/writings/taoup/html/apb.html#Vo "[Vo]")\].

Under Unix, it is normal practice to make this layering explicit, with the service routines collected in a library that is separately documented. In such programs, the front end gets to specialize in user-interface considerations and high-level protocol. With a little more care in design, it may be possible to detach the original front end and replace it with others adapted for different purposes. Some other advantages should become evident from our case study.

There is a flip side to this. In the Unix world, libraries which are delivered [*as libraries*]{.emphasis} should come with exerciser programs.

::: blockquote
  ------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                            APIs should come with programs, and vice versa. An API that you must write C code to use, which cannot be invoked easily from the command line, is harder to learn and use. And contrariwise, it\'s a royal pain to have interfaces whose [*only*]{.emphasis} open, documented form is a program, so you cannot invoke them easily from a C program --- for example, route(1) in older Linuxes.    
  \--[ [Henry Spencer]{.author} []{#id2900299 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                      
  ------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Besides easing the learning curve, library exercisers often make excellent test frameworks. Experienced Unix programmers therefore see them not just as a form of thoughtfulness to the library\'s users but as an indication that the code has probably been well tested.

An important form of library layering is the *plugin*, a library with a set of known entry points that is dynamically loaded after startup time to perform a specialized task. For plugins to work, the calling program has to be organized largely as a documented service library that the plugin can call back into.

::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#gimp_plugins}Case Study: GIMP Plugins {#case-study-gimp-plugins .title}

</div>
::::

[]{#id2900365 .indexterm}

The GIMP (GNU Image Manipulation program)[]{#id2900380 .indexterm} is a graphics editor designed to be driven through an interactive GUI. But GIMP is built as a library of image-manipulation and housekeeping routines called by a relatively thin layer of control code. The driver code knows about the GUI, but not directly about image formats; the library routines reverse this by knowing about image formats and operations but not about the GUI.

The library layer is documented (and, in fact shipped as "libgimp" for use by other programs). This means that C programs called "plugins" can be dynamically loaded by GIMP and call the library to do image manipulation, effectively taking over control at the same level as the GUI (see [Figure 4.2](ch04s04.html#libgimp "Figure 4.2. Caller/callee relationships in GIMP with a plugin loaded.")).

:::: figure
[]{#libgimp}

**Figure 4.2. Caller/callee relationships in GIMP with a plugin loaded.**

::: mediaobject
![Caller/callee relationships in GIMP with a plugin loaded.](http://www.catb.org/~esr/writings/taoup/html/graphics/gimp-org.png)
:::
::::

Plugins are used to perform lots of special-purpose transformations such as colormap hacking, blurring and despeckling; also for reading and writing file formats not native to the GIMP core; for extensions like editing animations and window manager themes; and for lots of other sorts of image-hacking that can be automated by scripting the image-hacking logic in the GIMP core. A registry of GIMP plugins is available on the World Wide Web.

Though most GIMP plugins are small, simple C[]{#id2900491 .indexterm} programs, it is also possible to write a plugin that exposes the library API to a scripting language[]{#id2900501 .indexterm}; we\'ll discuss this possibility in [Chapter 11](interfacechapter.html "Chapter 11. Interfaces") when we examine the 'polyvalent program' pattern.
:::::::
:::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- --------------------------------------------- ------------------------------------------
  [Prev](ch04s03.html){accesskey="p"}     [Up](modularitychapter.html){accesskey="u"}     [Next](unix_and_oo.html){accesskey="n"}
  Software Is a Many-Layered Thing             [Home](index.html){accesskey="h"}               Unix and Object-Oriented Languages
  -------------------------------------- --------------------------------------------- ------------------------------------------
:::
