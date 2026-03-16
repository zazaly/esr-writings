::: navheader
  Environment Variables                                              
  -------------------------------------- --------------------------- --------------------------------------
  [Prev](ch10s03.html){accesskey="p"}     Chapter 10. Configuration     [Next](ch10s05.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2942386}Environment Variables {#environment-variables .title style="clear: both"}

</div>
::::

When a Unix program starts up, the environment accessible to it includes a set of name to value associations (names and values are both strings). Some of these are set manually by the user; others are set by the system at login time, or by your shell or terminal emulator (if you\'re running one). Under Unix, environment variables tend to carry information about file search paths, system defaults, the current user ID and process number, and other key bits of information about the runtime einvironment of programs. At a shell prompt, typing **set** followed by a newline will list all currently defined shell variables.

In C[]{#id2942417 .indexterm} and C++[]{#id2942425 .indexterm} these values can be queried with the library function getenv(3). Perl[]{#id2942443 .indexterm} and Python[]{#id2942451 .indexterm} initialize environment-dictionary objects at startup. Other languages generally follow one of these two models.

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2942463}System Environment Variables {#system-environment-variables .title}

</div>
::::

There are a number of well-known environment variables you can expect to find defined on startup of a program from the Unix shell. These (especially `HOME`) will often need to be evaluated [*before*]{.emphasis} you read a local dotfile.

::: variablelist

[`USER`]{.term}

:   Login name of the account under which this session is logged in (BSD convention).

[`LOGNAME`]{.term}

:   Login name of the account under which this session is logged in (System V []{#id2942519 .indexterm} convention).

[`HOME`]{.term}

:   Home directory of the user running this session.

[`COLUMNS`]{.term}

:   The number of character-cell columns on the controlling terminal or terminal-emulator window.

[`LINES`]{.term}

:   The number of character-cell rows on the controlling terminal or terminal-emulator window.

[`SHELL`]{.term}

:   The name of the user\'s command shell (often used by shellout commands).

[`PATH`]{.term}

:   The list of directories that the shell searches when looking for executable commands to match a name.

[`TERM`]{.term}

:   Name of the terminal type of the session console or terminal emulator window (see the terminfo case study in [Chapter 6](transparencychapter.html "Chapter 6. Transparency") for background). TERM is special in that programs to create remote sessions over the network (such as *telnet* and *ssh*) are expected to pass it through and set it in the remote session.
:::

(This list is representative, but not exhaustive.)

The `HOME` variable is especially important, because many programs use it to find the calling user\'s dotfiles (others call some functions in the C[]{#id2942669 .indexterm} runtime library to get the calling user\'s home directory).

Note that some or all of these system environment variables may [*not*]{.emphasis} be set when a program is started by some other method than a shell spawn. In particular, daemon listeners on a TCP/IP[]{#id2942690 .indexterm} socket often don\'t have these variables set --- and if they do, the values are unlikely to be useful.

Finally, note that there is a tradition (exemplified by the `PATH` variable) of using a colon as a separator when an environment variable must contain multiple fields, especially when the fields can be interpreted as a search path of some sort. Note that some shells (notably *bash* and *ksh*) [*always*]{.emphasis} interpret colon-separated fields in an environment variable as filenames, which means in particular that they expand `~` in these fields to the user\'s home directory.
::::::

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2942749}User Environment Variables {#user-environment-variables .title}

</div>
::::

Although applications are free to interpret environment variables outside the system-defined set, it is nowadays fairly unusual to actually do so. Environment values are not really suitable for passing structured information into a program (though it can in principle be done via parsing of the values). Instead, modern Unix applications tend to use run-control files and dotfiles.

There are, however, some design patterns in which user-defined environment variables can be useful:

[*Application-independent preferences that need to be shared by a large number of different programs.*]{.emphasis} This set of 'standard' preferences changes only slowly, because lots of different programs need to recognize each one before it becomes useful.^\[[102](ch10s04.html#ftn.id2942782){#id2942782}\]^ Here are the standard ones:

::: variablelist

[`EDITOR`]{.term}

:   The name of the user\'s preferred editor (often used by shellout commands).^\[[103](ch10s04.html#ftn.id2942810){#id2942810}\]^

[`MAILER`]{.term}

:   The name of the user\'s preferred mail user agent (often used by shellout commands).

[`PAGER`]{.term}

:   The name of the user\'s preferred program for browsing plaintext.

[`BROWSER`]{.term}

:   The name of the user\'s preferred program for browsing Web URLs. This one, as of 2003, is still very new and not yet widely implemented.
:::
::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2942882}When to Use Environment Variables {#when-to-use-environment-variables .title}

</div>
::::

What both user and system environment variables have in common is that it would be annoying to have to replicate the information they contain in a large number of application run-control files, and extremely annoying to have to change that information everywhere when your preference changes. Typically, the user sets these variables in his or her shell session startup file.

[*A value varies across several contexts that share dotfiles, or a parent needs to pass information to multiple child processes.*]{.emphasis} Some pieces of start-up information are expected to vary across several contexts in which the calling user would share common run-control files and dotfiles. For a system-level example, consider several shell sessions open through terminal emulator windows on an X desktop. They will all see the same dotfiles, but might have different values of `COLUMNS`, `LINES`, and `TERM`. (Old-school shell programming used this method extensively; makefiles still do.)

[*A value varies too often for dotfiles, but doesn\'t change on every startup.*]{.emphasis} A user-defined environment variable may (for example) be used to pass a file system or Internet location that is the root of a tree of files that the program should play with. The CVS version-control system interprets the variable `CVSROOT` this way, for example. Several newsreader clients that fetch news from servers using the NNTP protocol interpret the variable `NNTPSERVER` as the location of the server to query.

[*A process-unique override needs to be expressed in a way that doesn\'t require the command-line invocation to be changed.*]{.emphasis} A user-defined environment variable can be useful for situations in which, for whatever reason, it would be inconvenient to have to change an application dotfile or supply command-line options (perhaps it is expected that the application will normally be used inside a shell wrapper or within a makefile). A particularly important context for this sort of use is debugging. Under Linux, for example, manipulating the variable `LD_LIBRARY_PATH` associated with the ld(1) linking loader enables you to change where libraries are loaded from --- perhaps to pick up versions that do buffer-overflow checking or profiling.

In general, a user-defined environment variable can be an effective design choice when the value changes often enough to make editing a dotfile each time inconvenient, but not necessarily every time (so always setting the location with a command-line option would also be inconvenient). Such variables should typically be evaluated [*after*]{.emphasis} a local dotfile and be permitted to override settings in it.

There is one traditional Unix design pattern that we do not recommend for new programs. Sometimes, user-set environment variables are used as a lightweight substitute for expressing a program preference in a run-control file. The venerable nethack(1) dungeon-crawling game, for example, reads a `NETHACKOPTIONS` environment variable for user preferences. This is an old-school technique; modern practice would lean toward parsing them from a `.nethack` or `.nethackrc` run-control file.

The problem with the older style is that it makes tracking where your preference information lives more difficult than it would be if you knew the program had a run-control file under your home directory. Environment variables can be set anywhere in several different shell run-control files --- under Linux these are likely to include `.profile`, `.bash_profile`, and `.bashrc` at least. These files are cluttered and fragile things, so as the code overhead of having an option-parser has come to seem less significant preference information has tended to migrate out of environment variables into dotfiles.
:::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2947980}Portability to Other Operating Systems {#portability-to-other-operating-systems .title}

</div>
::::

Environment variables have only very limited portability off Unix. Microsoft operating systems[]{#id2947991 .indexterm} have an environment-variable feature modeled on that of Unix, and use a `PATH` variable as Unix does to set the binary search path, but most of other variables that Unix shell programmers take for granted (such as process ID or current working directory) are not supported. Other operating systems (including classic MacOS) generally do not have any local equivalent of environment variables.
:::::

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[102](ch10s04.html#id2942782){#ftn.id2942782}\]^ Nobody knows a really graceful way to represent this sort of distributed preference data; environment variables probably are not it, but all the known alternatives have equally nasty problems.
:::

::: footnote
^\[[103](ch10s04.html#id2942810){#ftn.id2942810}\]^ Actually, most Unix programs first check `VISUAL`, and only if that\'s not set will they consult `EDITOR`. That\'s a relic from the days when people had different preferences for line-oriented editors and visual editors.
:::
:::::
::::::::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ------------------------------------------------ --------------------------------------
  [Prev](ch10s03.html){accesskey="p"}     [Up](configurationchapter.html){accesskey="u"}     [Next](ch10s05.html){accesskey="n"}
  Run-Control Files                             [Home](index.html){accesskey="h"}                           Command-Line Options
  -------------------------------------- ------------------------------------------------ --------------------------------------
:::
