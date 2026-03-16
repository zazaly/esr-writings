::: navheader
  How to Choose among the Methods                                    
  -------------------------------------- --------------------------- --------------------------------------
  [Prev](ch10s05.html){accesskey="p"}     Chapter 10. Configuration     [Next](ch10s07.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2950195}How to Choose among the Methods {#how-to-choose-among-the-methods .title style="clear: both"}

</div>
::::

We\'ve looked in turn at system and user run-control files, at environment variables, and at command-line arguments. Observe the progression from least easily changed to most easily changed. There is a strong convention that well-behaved Unix programs that use more than one of these places should look at them in the order given, allowing later settings to override earlier ones (there are specific exceptions, such as command-line options that specify where a dotfile should be found).

In particular, environment settings usually override dotfile settings, but can be overridden by command-line options. It is good practice to provide a command-line option like the `-e` of make(1) that can override environment settings or declarations in run-control files; that way the program can be scripted with well-defined behavior regardless of the way the run-control files look or environment variables are set.

Which of these places you choose to look at depends on how much persistent configuration state your program needs to keep around between invocations. Programs designed mainly to be used in a batch mode (as generators or filters in pipelines, for example) are usually completely configured with command-line options. Good examples of this pattern include ls(1), grep(1) and sort(1). At the other extreme, large programs with complicated interactive behavior may rely entirely on run-control files and environment variables, and normal use involves few command-line options or none at all. Most X window managers are a good example of this pattern.

(Unix has the capability for the same file to have multiple names or 'links'. At startup time, every program has available to it the filename through which it was called. One other way to signal to a program that has several modes of operation which one it should come up in is to give it a link for each mode, have it find out which link it was called through, and change its behavior accordingly. But this technique is generally considered unclean and seldom used.)

Let\'s look at a couple of programs that gather configuration data from all three places. It will be instructive to consider why, for each given piece of configuration data, it is collected as it is.

::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#fetchmail_environment}Case Study: *fetchmail* {#case-study-fetchmail .title}

</div>
::::

[]{#id2950315 .indexterm}

The *fetchmail* program uses only two environment variables, `USER` and `HOME`. These variables are in the predefined set initialized by the system; many programs use them.

The value of `HOME` is used to find the dotfile `.fetchmailrc`, which contains configuration information in a fairly elaborate syntax obeying the shell-like lexical rules described above. This is appropriate because, once it has been initially set up, Fetchmail\'s configuration will change only infrequently.

There is neither an `/etc/fetchmailrc` nor any other systemwide file specific to fetchmail. Normally such files hold configuration that\'s not specific to an individual user. fetchmail does use a small set of properties with this kind of scope --- specifically, the name of the local postmaster, and a few switches and values describing the local mail transport setup (such as the port number of the local SMTP listener). In practice, however, these are seldom changed from their compiled-in default values. When they are changed, they tend to be modified in user-specific ways. Thus, there has been no demand for a systemwide fetchmail run-control file.

Fetchmail can retrieve host/login/password triples from a `.netrc` file. Thus, it gets authenticator information in the least surprising way.

Fetchmail has an elaborate set of command-line options, which nearly but do not entirely replicate what the `.fetchmailrc` can express. The set was not originally large, but grew over time as new constructs were added to the `.fetchmailrc` minilanguage and parallel command-line options for them were added more or less reflexively.

The intent of supporting all these options was to make fetchmail easier to script by allowing users to override bits of its run control from the command line. But it turns out that outside of a few options like `--fetchall` and `--verbose` there is little demand for this --- and none that can\'t be satisfied with a shellscript that creates a temporary run-control file on the fly and then feeds it to fetchmail using the `-f` option.

Thus, most of the command-line options are never used, and in retrospect including them was probably a mistake; they bulk up the fetchmail code a bit without accomplishing anything very useful.

::: blockquote
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                           If bulking up the code were the only problem, nobody would care, except for a couple of maintainers. However, options increase the chances of error in code, particularly due to unforeseen interactions among rarely used options. Worse, they bulk up the manual, which is a burden on everybody.    
  \--[ [Doug McIlroy]{.author} []{#id2950474 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                          
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

There is a lesson here; had I thought carefully enough about fetchmail\'s usage pattern and been a little less ad-hoc about adding features, the extra complexity might have been avoided.

::: blockquote
  ------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ ---
                                                                            An alternative way of dealing with such situations, which doesn\'t clutter up either the code or the manual much, is to have a "set option variable" option, such as the `-O` option of *sendmail*, which lets you specify an option name and value, and sets that name to that value as if such a setting had been given in a configuration file. A more powerful variant of this is what *ssh* does with its `-o` option: the argument to `-o` is treated as if it were a line appended to the configuration file, with the full config-file syntax available. Either of these approaches gives people with unusual requirements a way to override configuration from the command line, without requiring you to provide a separate option for each bit of configuration that might be overridden.    
  \--[ [Henry Spencer]{.author} []{#id2950516 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           
  ------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ ---
:::
:::::::

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2950578}Case Study: The XFree86 Server {#case-study-the-xfree86-server .title}

</div>
::::

The X windowing system is the engine that supports bitmapped displays on Unix machines. Unix applications running through a client machine with a bitmapped display get their input events through X and send screen-painting requests to it. Confusingly, X 'servers' actually run on the client machine --- they exist to serve requests to interact with the client machine\'s display device. The applications sending those requests to the X server are called 'X clients', even though they may be running on a server machine. And no, there is no way to explain this inverted terminology that is not confusing.

X servers have a forbiddingly complex interface to their environment. This is not surprising, as they have to deal with a wide range of complex hardware and user preferences. The environment queries common to all X servers, documented on the X(1) and Xserver(1) pages, therefore make a useful example for study. The implementation we examine here is XFree86, the X implementation used under Linux[]{#id2950627 .indexterm} and several other open-source Unixes.

At startup, the XFree86 server examines a systemwide run-control file; the exact pathname varies between X builds on different platforms, but the basename is XF86Config. The XF86Config file has a shell-like syntax as described above. [Example 10.2](ch10s06.html#X_config "Example 10.2. X configuration example.") is a sample section of an XF86Config file.

::: example
[]{#X_config}

**Example 10.2. X configuration example.**

``` programlisting
# The 16-color VGA server

Section "Screen"
    Driver      "vga16"
    Device      "Generic VGA"
    Monitor     "LCD Panel 1024x768"
    Subsection  "Display"
        Modes       "640x480" "800x600"
        ViewPort    0 0
    EndSubsection
EndSection
```
:::

The XF86Config file describes the host machine\'s display hardware (graphics card, monitor), keyboard, and pointing device (mouse/trackball/glidepad). It\'s appropriate for this information to live in a systemwide run-control file, because it applies to all users of the machine.

Once X has acquired its hardware configuration from the run control file, it uses the value of the environment variable `HOME` to find two dotfiles in the calling user\'s home directory. These files are `.Xdefaults` and `.xinitrc`.^\[[105](ch10s06.html#ftn.id2950710){#id2950710}\]^

The `.Xdefaults` file specifies per-user, application-specific resources relevant to X (trivial examples of these might include font and foreground/background colors for a terminal emulator). The phrase 'relevant to X' indicates a design problem, however. Collecting all these resource declarations in one place is convenient for inspecting and editing them, but it is not always clear what should be declared in `.Xdefaults` and what belongs in an application-specific dotfile. The `.xinitrc` file specifies the commands that should be run to initialize the user\'s X desktop just after server startup. These programs will almost always include a window or session manager.

X servers have a large set of command-line options. Some of these, such as the `-fp` (font path) option, override the XF86Config. Some are intended to help track server bugs, such as the `-audit` option; if these are used at all, they are likely to vary quite frequently between test runs and are therefore poor candidates to be included in a run-control file. A very important option is the one that sets the server\'s display number. Multiple servers may run on a host provided each has a unique display number, but all instances share the same run-control file(s); thus, the display number cannot be derived solely from those files.
::::::

:::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[105](ch10s06.html#id2950710){#ftn.id2950710}\]^ The `.xinitrc` is analogous to a Startup folder on Windows and other operating systems.
:::
::::
::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ------------------------------------------------ --------------------------------------
  [Prev](ch10s05.html){accesskey="p"}     [Up](configurationchapter.html){accesskey="u"}     [Next](ch10s07.html){accesskey="n"}
  Command-Line Options                          [Home](index.html){accesskey="h"}                        On Breaking These Rules
  -------------------------------------- ------------------------------------------------ --------------------------------------
:::
