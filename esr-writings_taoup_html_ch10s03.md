::: navheader
  Run-Control Files                                                  
  -------------------------------------- --------------------------- --------------------------------------
  [Prev](ch10s02.html){accesskey="p"}     Chapter 10. Configuration     [Next](ch10s04.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2941824}Run-Control Files {#run-control-files .title style="clear: both"}

</div>
::::

A run-control file is a file of declarations or commands associated with a program that it interprets on startup. If a program has site-specific configuration shared by all users at a site, it will often have a run-control file under the `/etc` directory. (Some Unixes have an `/etc/conf` subdirectory that collects such data.)

User-specific configuration information is often carried in a hidden run-control file in the user\'s home directory. Such files are often called 'dotfiles' because they exploit the Unix convention that a filename beginning with a dot is normally invisible to directory-listing tools.^\[[100](ch10s03.html#ftn.id2941866){#id2941866}\]^

Programs can also have run-control or dot directories. These group together several configuration files that are related to the program, but that are most conveniently treated separately (perhaps because they relate to different subsystems of the program, or have differing syntaxes).

Whether file or directory, convention now dictates that the location of the run-control information has the same basename as the executable that reads it. An older convention still common among system programs uses the executable\'s name with the suffix 'rc' for 'run control'.^\[[101](ch10s03.html#ftn.id2941902){#id2941902}\]^ Thus, if you write a program called 'seekstuff' that has both site-wide and user-specific configuration, an experienced Unix user would expect to find the former at `/etc/seekstuff` and the latter at `.seekstuff` in the user\'s home directory; but it would be unsurprising if the locations were `/etc/seekstuffrc` and `.seekstuffrc`, especially if seekstuff were a system utility of some sort.

In [Chapter 5](textualitychapter.html "Chapter 5. Textuality") we described a somewhat different set of design rules for textual data-file formats, and discussed how to optimize for different weightings of interoperability, transparency[]{#id2941968 .indexterm} and transaction economy. Run-control files are typically only read once at program startup and not written; economy is therefore usually not a major concern. Interoperability and transparency both push us toward textual formats designed to be read by human beings and modified with an ordinary text editor.

While the semantics of run-control files are of course completely program dependent, there are some design rules about run-control syntax that are widely observed. We\'ll describe those next; but first we\'ll describe an important exception.

If the program is an interpreter for a language, then it is expected to be simply a file of commands in the syntax of that language, to be executed at startup. This is an important rule, because Unix tradition strongly encourages the design of all kinds of programs as special-purpose languages and minilanguages. Well-known examples with dotfiles of this kind include the various Unix command shells and the *Emacs* programmable editor.

(One reason for this design rule is the belief that special cases are bad news --- thus, that any switch that changes the behavior of a language should be settable from within the language. If as a language designer you find that you [*cannot*]{.emphasis} express all the startup settings of a language in the the language itself, a Unix programmer would say you have a design problem --- which is what you should be fixing, rather than devising a special-case run-control syntax.)

This exception aside, here are the normal style rules for run-control syntaxes. Historically, they are patterned on the syntax of Unix shells:

::: orderedlist
1.  [*Support explanatory comments, and lead them with `#`.*]{.emphasis} The syntax should also ignore whitespace before `#`, so that comments on the same line as configuration directives are supported.

2.  [*Don\'t make insidious whitespace distinctions.*]{.emphasis} That is, treat runs of spaces and tabs, syntactically the same as a single space. If your directive format is line-oriented, it is good form to ignore trailing spaces and tabs on lines. The metarule is that the interpretation of the file should not depend on distinctions a human eye can\'t see.

3.  [*Treat multiple blank lines and comment lines as a single blank line*]{.emphasis}. If the input format uses blank lines as separators between records, you probably want to ensure that a comment line does not end a record.

4.  [*Lexically treat the file as a simple sequence of whitespace-separated tokens, or lines of tokens.*]{.emphasis} Complicated lexical rules are hard to learn, hard to remember, and hard for humans to parse. Avoid them.

5.  [*But, support a string syntax for tokens with embedded whitespace.*]{.emphasis} Use single quote or double quote as balanced delimiters. If you support both, beware of giving them different semantics as they have in shell; this is a well-known source of confusion.

6.  [*Support a backslash syntax for embedding unprintable and special characters in strings*]{.emphasis}. The standard pattern for this is the backslash-escape syntax supported by C compilers. Thus, for example, it would be quite surprising if the string `"a\tb"` were not interpreted as a character 'a', followed by a tab, followed by the character 'b'.
:::

Some aspects of shell syntax, on the other hand, should [*not*]{.emphasis} be emulated in run-control syntaxes --- at least not without a good and specific reason. The shell\'s baroque quoting and bracketing rules, and its special metacharacters for wildcards and variable substitution, both fall into this category.

It bears repeating that the point of these conventions is to reduce the amount of novelty that users have to cope with when they read and edit the run-control file for a program they have never seen before. Therefore, if you have to break the conventions, try to do so in a way that makes it visually obvious that you have done so, document your syntax with particular care, and (most importantly) design it so it\'s easy to pick up by example.

These standard style rules only describe conventions about tokenizing and comments. The names of run-control files, their higher-level syntax, and the semantic interpretation of the syntax are usually application-specific. There are a very few exceptions to this rule, however; one is dotfiles which have become 'well-known' in the sense that they routinely carry information used by a whole class of applications. Sharing run-control file formats in this way reduces the amount of novelty users have to cope with.

Of these, probably the best established is the `.netrc` file. Internet client programs that must track host/password pairs for a user can usually get them from the `.netrc` file, if it exists.

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2942210}Case Study: The `.netrc` File {#case-study-the-.netrc-file .title}

</div>
::::

The `.netrc` file is a good example of the standard rules in action. An example, with the passwords changed to protect the innocent, is in [Example 10.1](ch10s03.html#netrc "Example 10.1. A .netrc example.").

::: example
[]{#netrc}

**Example 10.1. A `.netrc` example.**

``` programlisting
# FTP access to my Web host
machine unix1.netaxs.com
        login esr
        password joesatriani

# My main mailserver at Netaxs
machine imap.netaxs.com
        login esr
        password jeffbeck

# Auxiliary IMAP maildrop at CCIL
machine imap.ccil.org
    login esr
    password marcbonilla

# Auxiliary POP maildrop at CCIL
machine pop3.ccil.org
    login esr
    password ericjohnson

# Shell account at CCIL
machine locke.ccil.org
    login esr
    password stevemorse
```
:::

Observe that this format is easy to parse by eyeball even if you\'ve never seen it before; it\'s a set of machine/login/password triples, each of which describes an account on a remote host. This kind of transparency[]{#id2942282 .indexterm} is important --- much more important, actually, than the time economy of faster interpretation or the space economy of a more compact and cryptic file format. It economizes the far more valuable resource that is [*human*]{.emphasis} time, by making it likely that a human being will be able to read and modify the format without having to read a manual or use a tool less familiar than a plain old text editor.

Observe also that this format is used to supply information for multiple services --- an advantage, because it means sensitive password information need only be stored in one place. The `.netrc` format was designed for the original Unix FTP client program. It\'s used by all FTP clients, and also understood by some telnet clients, and by the smbclient(1) command-line tool, and by the *fetchmail*[]{#id2942337 .indexterm} program. If you are writing an Internet client that must do password authentication through remote logins, the Rule of Least Surprise demands that it use the contents of `.netrc` as defaults.
::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2942358}Portability to Other Operating Systems {#portability-to-other-operating-systems .title}

</div>
::::

Systemwide run-control files are a design tactic that can be used on almost any operating system, but dotfiles are rather more difficult to map to a non-Unix environment. The critical thing missing from most non-Unix operating systems is true multiuser capability and the notion of a per-user home directory. DOS and Windows versions up to ME (including 95 and 98), for example, completely lack any such notion; all configuration information has to be stored either in systemwide run-control files at a fixed location, the Windows registry, or configuration files in the same directory a program is run from. Windows NT has some notion of per-user home directories (which made its way into Windows 2000 and XP), but it is only poorly supported by the system tools.
:::::

::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[100](ch10s03.html#id2941866){#ftn.id2941866}\]^ To make dotfiles visible, use the `-a` option of ls(1).
:::

::: footnote
^\[[101](ch10s03.html#id2941902){#ftn.id2941902}\]^ The 'rc' suffix goes back to Unix\'s grandparent, CTSS[]{#id2941907 .indexterm}. It had a command-script feature called \"runcom\". Early Unixes used 'rc' for the name of the operating system\'s boot script, as a tribute to CTSS runcom.
:::
:::::
::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ------------------------------------------------ --------------------------------------
  [Prev](ch10s02.html){accesskey="p"}     [Up](configurationchapter.html){accesskey="u"}     [Next](ch10s04.html){accesskey="n"}
  Where Configurations Live                     [Home](index.html){accesskey="h"}                          Environment Variables
  -------------------------------------- ------------------------------------------------ --------------------------------------
:::
