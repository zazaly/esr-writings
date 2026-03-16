::: {#Header}
  ---------------------------------------- --
  Errata for The Art of Unix Programming   
  ---------------------------------------- --
:::

::: {#Menu}

------------------------------------------------------------------------

[Home Page](http://www.catb.org/~esr "My home page")\
[Site Map](http://www.catb.org/~esr/sitemap.html "Map of the site")\
[TAOUP](index.html)\
[Contributing](contribute.html)\

------------------------------------------------------------------------
:::

::: {#Content}
# Corrections:

-   Bryce Kampjes point out: \"In the section TCP/IP and the Unix Wars: 1980-1990 in the discussion about the emergence of the 386 there is no mention of the RISC machines. At the time, it did look like the old x86 architecture was going to run out of steam, a 1 million transistor 486 could barely compete with 100,000 transistor RISC chips. If that trend continued, then the x86 would have been history. But the market could afford to throw large amounts of money to make a bad architecture perform.\"

-   Graham J Lee: \"I was quite surprised that the ultimate in counter-examples, find(1), was not covered in depth as it was applicable in a few places as a description of how UNIX programs should \*not\* be done. For instance, it contains code to mimic the results of other UNIX programs, such as cpio or ls, when it could easily have been combined with these programs via pipes and xargs. It also has a \*very\* non-standard interface, with X style option flags despite having been created very early in the history of UNIX.\"

# Things to add, maybe:

-   There is a good article on X toolkit comparisons [here](http://freshmeat.net/articles/view/928).

-   Diomedis Spinellis notes that an interesting case study for the Interfaces chapter would be the addition of a GUI front-end to a command-line driven debugger engine. The front-end typically sends commands to the debugger and interprets the response. Dbxtool was an early example, xgdb a follower. He points to [this paper](http://citeseer.nj.nec.com/context/157910/0).

-   Diomedis also notes: Another case where a shell script is preferable is when it is used to construct a pipeline of commands that offer facilities not typically available as part of a language library (it is getting more difficult as time goes by to find such cases). Consider:

        find ... |
        while read i
        do
                gzip -dc $i
        done |
        sed -e ... |
        tsort |
        join

    He notes: \"You can do find and sed in Perl and gunzip in Java, but I have yet to see a topological sort or join function in a standard library.\"

-   Cite his
    critique of the Windows API.
    How much of this has changed since?

-   Here is an example for a new topic: how the fact that the shell is an ordinary program, and can be invoked recusively, is helpful.

        /usr/bin/script -c "PS1='script:\u@\h:\w\$ ' /bin/sh"

-   James Hunt\'s clever [application of make](http://www-106.ibm.com/developerworks/linux/library/l-boot.html?ca=dgr-lnxw04BootFaster) to speeding up the Unix boot process could be a case study.

-   Cover [asciidoc](http://www.methods.co.nz/asciidoc/). A very Unixy, lightweight solution to the document-markup problem which might relegate DocBook to the role of a transport and interchange format.

-   Cover [YAML](http://www.yaml.org/). Nice lightweight alternative to XML for structured-data interchange; the fact that its data model is structures and sequences rather than attributed trees is interesting.

-   Rich Morin: \"Other problems with shell as a programming language include the difficulty of getting complex quoting combinations right and the difficulty of passing multiple results back from a script to its invoker.\"

-   Rich Morin: \"Part of the problem with C++ was commercial/sociological; because the early developers couldn\'t agree on common, free libraries, no standard libraries developed.\"

-   Rich Morin: \"Markup languages have a hidden benefit over WYSIWYG systems: they allow (force, really) the author to examine the document in two different formats. This helps to defeat the \"snow blindness\" that keeps authors from spotting typos, etc.\"

-   Rich Morin: \"The discussion of POD neglects to mention that POD is capable of being embedded in Perl. This has been used to very good effect in getting module authors to write (and maintain) manual pages.\"

-   Rich Morin: \"The discussion in section 19.3 should explain a bit about the Berne Convention\'s effect on documents which have NO explicit copyright notice. In brief, they have a copyright which is too weak to be particularly useful, but strong enough to get in the way of the document\'s use by aggregators, open-source projects, etc.\"

-   Yet another reason for transparent textual formats: someone, somewhere, someday, is going to have to understand your format without having the documentation for it.

-   Discuss JavaDoc as a significant benefit of Java. (Done.)

-   In interface design, note that high variability in response latency is worse than moderate but consistent response latency.

-   Dr. David Alan Gilbert: \"there should be a strong health warning around \'Web browsers as the universal front end\'. Well it is true that they can be very useful, they tend to be implemented in a way which is harder to script. In addition where the application is implemented as a series of CGI scripts they place all the computational load on the server. I have recently seen a number of examples of programmers used to php/web programming pushing all the load onto a single web server when they all have respectably powerful Unix boxen under their desks.\"

-   On the other hand, AJAX may make Dr. Gilbert\'s health warning obsolete\...

-   IBM is using GPL as an affirmative defense in the SCO lawsuit. This will require iminor revisions in the last section of the Re-Use chapter.
:::
