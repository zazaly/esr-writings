::: navheader
  Taxonomy of Unix IPC Methods                                         
  -------------------------------------- ----------------------------- --------------------------------------
  [Prev](ch07s01.html){accesskey="p"}     Chapter 7. Multiprogramming     [Next](ch07s03.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2915457}Taxonomy of Unix IPC Methods {#taxonomy-of-unix-ipc-methods .title style="clear: both"}

</div>
::::

As in single-process program architectures, the simplest organization is the best. The remainder of this chapter will present IPC techniques roughly in order of escalating complexity of programming them. Before using a later, more complex technique, you should prove by demonstration --- with prototypes and benchmark results --- that no earlier and simpler technique will do. Often you will surprise yourself.

:::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2915475}Handing off Tasks to Specialist Programs {#handing-off-tasks-to-specialist-programs .title}

</div>
::::

In the simplest form of interprogram cooperation enabled by inexpensive process spawning, a program runs another to accomplish a specialized task. Because the called program is often specified as a Unix shell command through the system(3) call, this is often called [*shelling out*]{.emphasis} to the called program. The called program inherits the user\'s keyboard and display and runs to completion. When it exits, the calling program resumes control of the keyboard and display and resumes execution.^\[[68](ch07s02.html#ftn.id2915505){#id2915505}\]^ Because the calling program does not communicate with the called program during the callee\'s execution, protocol design is not an issue in this kind of cooperation, except in the trivial sense that the caller may pass command-line arguments to the callee to change its behavior.

The classic Unix case of shelling out is calling an editor from within a mail or news program. In the Unix tradition one does [*not*]{.emphasis} bundle purpose-built editors into programs that require general text-edited input. Instead, one allows the user to specify an editor of his or her choice to be called when editing needs to be done.

The specialist program usually communicates with its parent through the file system, by reading or modifying file(s) with specified location(s); this is how editor or mailer shellouts work.

In a common variant of this pattern, the specialist program may accept input on its standard input, and be called with the C[]{#id2915548 .indexterm} library entry point `popen(..., "w")` or as part of a shellscript. Or it may send output to its standard output, and be called with `popen(..., "r")` or as part of a shellscript. (If it both reads from standard input and writes to standard output, it does so in a batch mode, completing all reads before doing any writes.) This kind of child process is not usually referred to as a shellout; there is no standard jargon for it, but it might well be called a 'bolt-on'.

They key point about all these cases is that the specialist programs don\'t handshake with the parent while they are running. They have an associated protocol only in the trivial sense that whichever program (master or slave) is accepting input from the other has to be able to parse it.

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2915594}Case Study: The *mutt* Mail User Agent {#case-study-the-mutt-mail-user-agent .title}

</div>
::::

The *mutt*[]{#id2915615 .indexterm} mail user agent is the modern representative of the most important design tradition in Unix email programs. It has a simple screen-oriented interface with single-keystroke commands for browsing and reading mail.

When you use *mutt*[]{#id2915637 .indexterm} as a mail composer (either by calling it with an address as a command-line argument or by using one of the reply commands), it examines the process environment variable `EDITOR`, and then generates a temporary file name. The value of the `EDITOR` variable is called as a command with the tempfile name as an argument.^\[[69](ch07s02.html#ftn.id2915659){#id2915659}\]^ When that command terminates, *mutt* resumes on the assumption that the temporary file contains the desired mail text.

Almost all Unix mail- and netnews-composition programs observe the same convention. Because they do, composer implementers don\'t need to write a hundred inevitably diverging editors, and users don\'t need to learn a hundred divergent interfaces. Instead, users can carry their chosen editors with them.

An important variant of this strategy shells out to a small proxy program that passes the specialist job to an already-running instance of a big program, like an editor or a Web browser. Thus, developers who normally have an instance of *emacs* running on their X display can set **EDITOR=emacsclient**, and have a buffer pop open in their *emacs* when they request editing in *mutt*. The point of this is not really to save memory or other resources, it\'s to enable the user to unify all editing in a single *emacs* process (so that, for example, cut and paste among buffers can carry along internal *emacs* state information like font highlighting).
:::::
::::::::

:::::::::::::::::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#plumbing}Pipes, Redirection, and Filters {#pipes-redirection-and-filters .title}

</div>
::::

[]{#id2915769 .indexterm}[]{#id2915780 .indexterm}

After Ken Thompson[]{#id2915794 .indexterm} and Dennis Ritchie[]{#id2915802 .indexterm}, the single most important formative figure of early Unix was probably Doug McIlroy[]{#id2915812 .indexterm}. His invention of the [*pipe*]{.emphasis} construct reverberated through the design of Unix, encouraging its nascent do-one-thing-well philosophy and inspiring most of the later forms of IPC in the Unix design (in particular, the socket abstraction used for networking).

Pipes depend on the convention that every program has initially available to it (at least) two I/O data streams: standard input and standard output (numeric file descriptors 0 and 1 respectively). Many programs can be written as [*filters*]{.emphasis}, which read sequentially from standard input and write only to standard output.

Normally these streams are connected to the user\'s keyboard and display, respectively. But Unix shells universally support [*redirection*]{.emphasis} operations which connect these standard input and output streams to files. Thus, typing

``` programlisting
ls >foo
```

sends the output of the directory lister ls(1) to a file named 'foo'. On the other hand, typing:

``` programlisting
wc <foo
```

causes the word-count utility wc(1) to take its standard input from the file 'foo', and deliver a character/word/line count to standard output.

The pipe operation connects the standard output of one program to the standard input of another. A chain of programs connected in this way is called a [*pipeline*]{.emphasis}. If we write

``` programlisting
ls | wc
```

we\'ll see a character/word/line count for the current directory listing. (In this case, only the line count is really likely to be useful.)

::: blockquote
  ------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------- ---
                                                                           One favorite pipeline was "**bc \| speak**"---a talking desk calculator. It knew number names up to a vigintillion.    
  \--[ [Doug McIlroy]{.author} []{#id2915947 .indexterm} ]{.attribution}                                                                                                                          
  ------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------- ---
:::

It\'s important to note that all the stages in a pipeline run concurrently. Each stage waits for input on the output of the previous one, but no stage has to exit before the next can run. This property will be important later on when we look at interactive uses of pipelines, like sending the lengthy output of a command to more(1).

It\'s easy to underestimate the power of combining pipes and redirection. As an instructive example, *The Unix Shell As a 4GL* \[[Schaffer-Wolf](http://www.catb.org/~esr/writings/taoup/html/apb.html#Schaffer-Wolf "[Schaffer-Wolf]")\] shows that with these facilities as a framework, a handful of simple utilities can be combined to support creating and manipulating relational databases expressed as simple textual tables.

The major weakness of pipes is that they are unidirectional. It\'s not possible for a pipeline component to pass control information back up the pipe other than by terminating (in which case the previous stage will get a `SIGPIPE` signal on the next write). Accordingly, the protocol for passing data is simply the receiver\'s input format.

[]{#named_pipes} So far, we have discussed anonymous pipes created by the shell. There is a variant called a [*named pipe*]{.emphasis} which is a special kind of file. If two programs open the file, one for reading and the other for writing, a named pipe acts like a pipe-fitting between them. Named pipes are a bit of a historical relic; they have been largely displaced from use by named *sockets*, which we\'ll discuss below. (For more on the history of this relic, see the discussion of [System V IPC](ch07s03.html#messages "System V IPC") below.)

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2916058}Case Study: Piping to a Pager {#case-study-piping-to-a-pager .title}

</div>
::::

Pipelines have many uses. For one example, Unix\'s process lister ps(1) lists processes to standard output without caring that a long listing might scroll off the top of the user\'s display too quickly for the user to see it. Unix has another program, more(1), which displays its standard input in screen-sized chunks, prompting for a user keystroke after displaying each screenful.

Thus, if the user types "**ps \| more**", piping the output of ps(1) to the input of more(1), successive page-sized pieces of the list of processes will be displayed after each keystroke.

The ability to combine programs like this can be extremely useful. But the real win here is not cute combinations; it\'s that because both pipes and more(1) exist, [*other programs can be simpler*]{.emphasis}. Pipes mean that programs like ls(1) (and other programs that write to standard out) don\'t have to grow their own pagers --- and we\'re saved from a world of a thousand built-in pagers (each, naturally, with its own divergent look and feel). Code bloat is avoided and global complexity reduced.

As a bonus, if anyone needs to customize pager behavior, it can be done in [*one*]{.emphasis} place, by changing [*one*]{.emphasis} program. Indeed, multiple pagers can exist, and will all be useful with every application that writes to standard output.

In fact, this has actually happened. On modern Unixes, more(1) has been largely replaced by less(1), which adds the capability to scroll back in the displayed file rather than just forward.^\[[70](ch07s02.html#ftn.id2916197){#id2916197}\]^ Because less(1) is decoupled from the programs that use it, it\'s possible to simply alias 'more' to 'less' in your shell, set the environment variable `PAGER` to 'less' (see [Chapter 10](configurationchapter.html "Chapter 10. Configuration")), and get all the benefits of a better pager with all properly-written Unix programs.
:::::

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2916247}Case Study: Making Word Lists {#case-study-making-word-lists .title}

</div>
::::

A more interesting example is one in which pipelined programs cooperate to do some kind of data transformation for which, in less flexible environments, one would have to write custom code.

Consider the pipeline

``` programlisting
tr -c '[:alnum:]' '[\n*]' | sort -iu | grep -v '^[0-9]*$'
```

The first command translates non-alphanumerics on standard input to newlines on standard output. The second sorts lines on standard input and writes the sorted data to standard output, discarding all but one copy of spans of adjacent identical lines. The third discards all lines consisting solely of digits. Together, these generate a sorted wordlist to standard output from text on standard input.
:::::

:::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2916289}Case Study: *pic2graph* {#case-study-pic2graph .title}

</div>
::::

Shell source code for the program pic2graph(1) ships with the *groff* suite of text-formatting tools from the Free Software Foundation[]{#id2916320 .indexterm}. It translates diagrams written in the PIC language to bitmap images. [Example 7.1](ch07s02.html#pic2graph "Example 7.1. The pic2graph pipeline.") shows the pipeline at the heart of this code.

::: example
[]{#pic2graph}

**Example 7.1. The *pic2graph* pipeline.**

``` programlisting

(echo ".EQ"; echo $eqndelim; echo ".EN"; echo ".PS";cat;echo ".PE")|\
     groff -e -p $groffpic_opts -Tps >${tmp}.ps \
     && convert -crop 0x0 $convert_opts ${tmp}.ps ${tmp}.${format} \
     && cat ${tmp}.${format}
```
:::

The pic2graph(1) implementation illustrates how much one pipeline can do purely by calling preexisting tools. It starts by massaging its input into an appropriate form, continues by feeding it through groff(1) to produce PostScript, and finishes by converting the PostScript to a bitmap. All these details are hidden from the user, who simply sees PIC source go in one end and a bitmap ready for inclusion in a Web page come out the other.

This is an interesting example because it illustrates how pipes[]{#id2916399 .indexterm} and filtering can adapt programs to unexpected uses. The program that interprets PIC, pic(1), was originally designed only to be used for embedding diagrams in typeset documents. Most of the other programs in the toolchain it was part of are now semiobsolescent. But PIC remains handy for new uses, such as describing diagrams to be embedded in HTML. It gets a renewed lease on life because tools like pic2graph(1) can bundle together all the machinery needed to convert the output of pic(1) into a more modern format.

We\'ll examine pic(1) more closely, as a minilanguage design, in [Chapter 8](minilanguageschapter.html "Chapter 8. Minilanguages").
::::::

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2916464}Case Study: bc(1) and dc(1) {#case-study-bc1-and-dc1 .title}

</div>
::::

Part of the classic Unix toolkit dating back to Version 7 is a pair of calculator programs. The dc(1) program is a simple calculator that accepts text lines consisting of reverse-Polish notation (RPN) on standard input and emits calculated answers to standard output. The bc(1) program accepts a more elaborate infix syntax resembling conventional algebraic notation; it includes as well the ability to set and read variables and define functions for elaborate formulas.

While the modern GNU implementation of bc(1) is standalone, the classic version passed commands to dc(1) over a pipe. In this division of labor, bc(1) does variable substitution and function expansion and translates infix notation into reverse-Polish --- but doesn\'t actually do calculation itself, instead passing RPN translations of input expressions to dc(1) for evaluation.

There are clear advantages to this separation of function. It means that users get to choose their preferred notation, but the logic for arbitrary-precision numeric calculation (which is moderately tricky) does not have to be duplicated. Each of the pair of programs can be less complex than one calculator with a choice of notations would be. The two components can be debugged and mentally modeled independently of each other.

In [Chapter 8](minilanguageschapter.html "Chapter 8. Minilanguages") we will reexamine these programs from a slightly different example, as examples of domain-specific minilanguages.
:::::

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2921380}Anti-Case Study: Why Isn\'t *fetchmail* a Pipeline? {#anti-case-study-why-isnt-fetchmail-a-pipeline .title}

</div>
::::

In Unix terms, *fetchmail* is an uncomfortably large program that bristles with options. Thinking about the way mail transport works, one might think it would be possible to decompose it into a pipeline. Suppose for a moment it were broken up into several programs: a couple of fetch programs to get mail from POP3 and IMAP sites, and a local SMTP injector. The pipeline could pass Unix mailbox format. The present elaborate *fetchmail* configuration could be replaced by a shellscript containing command lines. One could even insert filters in the pipeline to block spam.

``` programlisting
#!/bin/sh
imap jrandom@imap.ccil.org | spamblocker | smtp jrandom
imap jrandom@imap.netaxs.com | smtp jrandom
# pop ed@pop.tems.com | smtp jrandom
```

This would be very elegant and Unixy. Unfortunately, it can\'t work. We touched on the reason earlier; pipelines are unidirectional.

One of the things the fetcher program (*imap* or *pop*) would have to do is decide whether to send a delete request for each message it fetches. In *fetchmail*\'s present organization, it can delay sending that request to the POP or IMAP server until it knows that the local SMTP listener has accepted responsibility for the message. The pipelined, small-component version would lose that property.

Consider, for example, what would happen if the *smtp* injector fails because the SMTP listener reports a disk-full condition. If the fetcher has already deleted the mail, we lose. This means the fetcher cannot delete mail until it is notified to do so by the *smtp* injector. This in turn raises a host of questions. How would they communicate? What message, exactly, would the injector pass back? The global complexity of the resulting system, and its vulnerability to subtle bugs, would almost certainly be higher than that of a monolithic program.

Pipelines are a marvelous tool, but not a universal one.
:::::
::::::::::::::::::::::

:::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2921506}Wrappers {#wrappers .title}

</div>
::::

The opposite of a shellout is a [*wrapper*]{.emphasis}. A wrapper creates a new interface for a called program, or specializes it. Often, wrappers are used to hide the details of elaborate shell pipelines[]{#id2921522 .indexterm}. We\'ll discuss interface wrappers in [Chapter 11](interfacechapter.html "Chapter 11. Interfaces"). Most specialization wrappers are quite simple, but nevertheless very useful.

As with shellouts, there is no associated protocol because the programs do not communicate during the execution of the callee; but the wrapper usually exists to specify arguments that modify the callee\'s behavior.

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2921550}Case Study: Backup Scripts {#case-study-backup-scripts .title}

</div>
::::

Specialization wrappers are a classic use of the Unix shell and other scripting languages[]{#id2921560 .indexterm}. One kind of specialization wrapper that is both common and representative is a backup script. It may be a one-liner as simple as this:

``` programlisting
tar -czvf /dev/st0 "$@"
```

This is a wrapper for the tar(1) tape archiver utility which simply supplies one fixed argument (the tape device `/dev/st0`) and passes to tar all the other arguments supplied by the user ("`$@`").^\[[71](ch07s02.html#ftn.id2921610){#id2921610}\]^
:::::
::::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2921634}Security Wrappers and Bernstein Chaining {#security-wrappers-and-bernstein-chaining .title}

</div>
::::

One common use of wrapper scripts is as *security wrappers*. A security script may call a gatekeeper program to check some sort of credential, then conditionally execute another based on the status value returned by the gatekeeper.

Bernstein chaining is a specialized security-wrapper technique first invented by Daniel J. Bernstein, who has employed it in a number of his packages. (A similar pattern appears in commands like nohup(1) and su(1), but the conditionality is absent.) Conceptually, a Bernstein chain is like a pipeline[]{#id2921677 .indexterm}, but each successive stage replaces the previous one rather than running concurrently with it.

The usual application is to confine security-privileged applications to some sort of gatekeeper program, which can then hand state to a less privileged one. The technique pastes several programs together using execs, or possibly a combination of forks and execs. The programs are all named on one command line. Each program performs some function and (if successful) runs exec(2) on the rest of its command line.

Bernstein\'s *rblsmtpd* package is a prototypical example. It serves to look up a host in the antispam DNS zone of the Mail Abuse Prevention System. It does this by doing a DNS query on the IP address passed into it in the `TCPREMOTEIP` environment variable. If the query is successful, then *rblsmtpd* runs its own SMTP that discards the mail. Otherwise the remaining command-line arguments are presumed to constitute a mail transport agent that knows the SMTP protocol, and are handed to exec(2) to be run.

Another example can be found in Bernstein\'s *qmail* package. It contains a program called *condredirect*. The first parameter is an email address, and the remainder a gatekeeper program and arguments. *condredirect* forks and execs the gatekeeper with its arguments. If the gatekeeper exits successfully, *condredirect* forwards the email pending on stdin to the specified email address. In this case, opposite to that of *rblsmtpd*, the security decision is made by the child; this case is a bit more like a classical shellout.

A more elaborate example is the *qmail* POP3 server. It consists of three programs, *qmail-popup*, *checkpassword*, and *qmail-pop3d*. *Checkpassword* comes from a separate package cleverly called *checkpassword*, and unsurprisingly it checks the password. The POP3 protocol has an authentication phase and mailbox phase; once you enter the mailbox phase you cannot go back to the authentication phase. This is a perfect application for Bernstein chaining.

The first parameter of *qmail-popup* is the hostname to use in the POP3 prompts. The rest of its parameters are forked and passed to exec(2), after the POP3 username and password have been fetched. If the program returns failure, the password must be wrong, so *qmail-popup* reports that and waits for a different password. Otherwise, the program is presumed to have finished the POP3 conversation, so *qmail-popup* exits.

The program named on *qmail-popup*\'s command line is expected to read three null-terminated strings from file descriptor 3.^\[[72](ch07s02.html#ftn.id2921897){#id2921897}\]^ These are the username, password, and response to a cryptographic challenge, if any. This time it\'s *checkpassword* which accepts as parameters the name of *qmail-pop3d* and its parameters. The *checkpassword* program exits with failure if the password does not match; otherwise it changes to the user\'s uid, gid, and home directory, and executes the rest of its command line on behalf of that user.

Bernstein chaining is useful for situations in which the application needs setuid or setgid privileges to initialize a connection, or to acquire some credential, and then drop those privileges so that following code does not have to be trusted. Following the exec, the child program cannot set its real user ID back to root. It\'s also more flexible than a single process, because you can modify the behavior of the system by inserting another program into the chain.

For example, *rblsmtpd* (mentioned above) can be inserted into a Bernstein chain, in between tcpserver (from the *ucspi-tcp* package) and the real SMTP server, typically *qmail-smtpd*. However, it works with inetd(8) and **sendmail -bs** as well.
:::::

:::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2922002}Slave Processes {#slave-processes .title}

</div>
::::

Occasionally, child programs both accept data from and return data to their callers through pipes[]{#id2922013 .indexterm} connected to standard input and output, interactively. Unlike simple shellouts and what we have called 'bolt-ons' above, both master and slave processes need to have internal state machines to handle a protocol between them without deadlocking or racing. This is a drastically more complex and more difficult-to-debug organization than a simple shellout.

Unix\'s popen(3) call can set up either an input pipe or an output pipe for a shellout, but not both for a slave process --- this seems intended to encourage simpler programming. And, in fact, interactive master-slave communication is tricky enough that it is normally only used when either (a) the implied protocol is utterly trivial, or (b) the slave process has been designed to speak an application protocol along the lines we discussed in [Chapter 5](textualitychapter.html "Chapter 5. Textuality"). We\'ll return to this issue, and ways to cope with it, in [Chapter 8](minilanguageschapter.html "Chapter 8. Minilanguages").

When writing a master/slave pair, it is good practice for the master to support a command-line switch or environment variable that allows callers to set their own slave command. Among other things, this is useful for debugging; you will often find it handy during development to invoke the real slave process from within a harness that monitors and logs transactions between slave and master.

If you find that master/slave interactions in your program are becoming nontrivial, it may be time to think about going the rest of the way to a more peer-to-peer organization, using techniques like sockets or shared memory.

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2922085}Case Study: *scp* and *ssh* {#case-study-scp-and-ssh .title}

</div>
::::

One common case in which the implied protocol really is trivial is progress meters. The scp(1) secure-copy command calls ssh(1) as a slave process, intercepting enough information from ssh\'s standard output to reformat the reports as an ASCII animation of a progress bar.^\[[73](ch07s02.html#ftn.id2922127){#id2922127}\]^
:::::
::::::::

::::::::::::::::::::::::::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2922148}Peer-to-Peer Inter-Process Communication {#peer-to-peer-inter-process-communication .title}

</div>
::::

All the communication methods we\'ve discussed so far have a sort of implicit hierarchy about them, with one program effectively controlling or driving another and zero or limited feedback passing in the opposite direction. In communications and networking we frequently need channels that are [*peer-to-peer*]{.emphasis}, usually (but not necessarily) with data flowing freely in both directions. We\'ll survey peer-to-peer communications methods under Unix here, and develop some case studies in later chapters.

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2922172}Tempfiles {#tempfiles .title}

</div>
::::

The use of tempfiles as communications drops between cooperating programs is the oldest IPC technique there is. Despite drawbacks, it\'s still useful in shellscripts, and in one-off programs where a more elaborate and coordinated method of communication would be overkill.

The most obvious problem with using tempfiles as an IPC technique is that it tends to leave garbage lying around if processing is interrupted before the tempfile can be deleted. A less obvious risk is that of collisions between multiple instances of a program using the same name for a tempfile. This is why it is conventional for shellscripts that make tempfiles to include \$\$ in their names; this shell variable expands to the process-ID of the enclosing shell and effectively guarantees that the filename will be unique (the same trick is supported in Perl).

Finally, if an attacker knows the location to which a tempfile will be written, it can overwrite on that name and possibly either read the producer\'s data or spoof the consumer process by inserting modified or spurious data into the file.^\[[74](ch07s02.html#ftn.id2922208){#id2922208}\]^ This is a security risk. If the processes involved have root privileges, this is a very serious risk. It can be mitigated by setting the permissions on the tempfile directory carefully, but such arrangements are notoriously likely to spring leaks.

All these problems aside, tempfiles still have a niche because they\'re easy to set up, they\'re flexible, and they\'re less vulnerable to deadlocks or race conditions than more elaborate methods. And sometimes, nothing else will do. The calling conventions of your child process may require that it be handed a file to operate on. Our first example of a shellout to an editor demonstrates this perfectly.
:::::

:::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2922239}Signals {#signals .title}

</div>
::::

The simplest and crudest way for two processes on the same machine to communicate with each other is for one to send the other a [*signal*]{.emphasis}. Unix signals are a form of soft interrupt; each one has a default effect on the receiving process (usually to kill it). A process can declare a [*signal handler*]{.emphasis} that overrides the default action for the signal; the handler is a function that is executed asynchronously when the signal is received.

Signals were originally designed into Unix as a way for the operating system to notify programs of certain errors and critical events, not as an IPC facility. The `SIGHUP` signal, for example, is sent to every program started from a given terminal session when that session is terminated. The `SIGINT` signal is sent to whatever process is currently attached to the keyboard when the user enters the currently-defined interrupt character (often control-C). Nevertheless, signals can be useful for some IPC situations (and the POSIX-standard signal set includes two signals, `SIGUSR1` and `SIGUSR2`, intended for this use)[]{#id2922305 .indexterm}. They are often employed as a control channel for [*daemons*]{.emphasis} (programs that run constantly, invisibly, in background), a way for an operator or another program to tell a daemon that it needs to either reinitialize itself, wake up to do work, or write internal-state/debugging information to a known location.

::: blockquote
+----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
|                                                                      | I insisted `SIGUSR1` and `SIGUSR2` be invented for BSD. People were grabbing system signals to mean what they needed them to mean for IPC, so that (for example) some programs that segfaulted would not coredump because `SIGSEGV` had been hijacked.                                                                          |                       |
|                                                                      |                                                                                                                                                                                                                                                                                                                                 |                       |
|                                                                      | This is a general principle --- people will want to hijack any tools you build, so you have to design them to either be un-hijackable or to be hijacked cleanly. Those are your only choices. Except, of course, for being ignored---a highly reliable way to remain unsullied, but less satisfying than might at first appear. |                       |
+----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
| \--[ [Ken Arnold]{.author} []{#id2922338 .indexterm} ]{.attribution} |                                                                                                                                                                                                                                                                                                                                 |                       |
+----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
:::

A technique often used with signal IPC is the so-called [*pidfile*]{.emphasis}. Programs that will need to be signaled will write a small file to a known location (often in `/var/run` or the invoking user\'s home directory) containing their process ID or PID. Other programs can read that file to discover that PID. The pidfile may also function as an implicit [*lock file*]{.emphasis} in cases where no more than one instance of the daemon should be running simultaneously.

There are actually two different flavors of signals. In the older implementations (notably V7, System III[]{#id2922421 .indexterm}, and early System V[]{#id2922430 .indexterm}), the handler for a given signal is reset to the default for that signal whenever the handler fires. The result of sending two of the same signal in quick succession is therefore usually to kill the process, no matter what handler was set.

The BSD 4.x []{#id2922447 .indexterm} versions of Unix changed to "reliable" signals, which do not reset unless the user explicitly requests it. They also introduced primitives to block or temporarily suspend processing of a given set of signals. Modern Unixes support both styles. You should use the BSD-style nonresetting entry points for new code, but program defensively in case your code is ever ported to an implementation that does not support them.

Receiving N signals does not necessarily invoke the signal handler N times. Under the older System V signal model, two or more signals spaced very closely together (that is, within a single timeslice of the target process) can result in various race conditions^\[[75](ch07s02.html#ftn.id2922479){#id2922479}\]^ or anomalies. Depending on what variant of signals semantics the system supports, the second and later instances may be ignored, may cause an unexpected process kill, or may have their delivery delayed until earlier instances have been processed (on modern Unixes the last is most likely).

The modern signals API is portable across all recent Unix versions, but not to Windows or classic (pre-OS X) MacOS.
::::::

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2922508}System Daemons and Conventional Signals {#system-daemons-and-conventional-signals .title}

</div>
::::

Many well-known system daemons accept `SIGHUP` (originally the signal sent to programs on a serial-line drop, such as was produced by hanging up a modem connection) as a signal to reinitialize (that is, reload their configuration files); examples include Apache[]{#id2922528 .indexterm} and the Linux implementations of bootpd(8), gated(8), inetd(8), mountd(8), named(8), nfsd(8), and ypbind(8). In a few cases, `SIGHUP` is accepted in its original sense of a session-shutdown signal (notably in Linux pppd(8)), but that role nowadays generally goes to `SIGTERM`.

`SIGTERM` ('terminate') is often accepted as a graceful-shutdown signal (this is as distinct from `SIGKILL`, which does an immediate process kill and cannot be blocked or handled). `SIGTERM` actions often involve cleaning up tempfiles, flushing final updates out to databases, and the like.

When writing daemons, follow the Rule of Least Surprise: use these conventions, and read the manual pages to look for existing models.
:::::

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#fetchmail_signals}Case Study: *fetchmail\'s* Use of Signals {#case-study-fetchmails-use-of-signals .title}

</div>
::::

[]{#id2922674 .indexterm}

The *fetchmail* utility is normally set up to run as a daemon in background, periodically collecting mail from all remote sites defined in its run-control file and passing the mail to the local SMTP listener on port 25 without user intervention. *fetchmail* sleeps for a user-defined interval (defaulting to 15 minutes) between collection attempts, so as to avoid constantly loading the network.

When you invoke **fetchmail** with no arguments, it checks to see if you have a *fetchmail* daemon already running (it does this by looking for a pidfile). If no daemon is running, *fetchmail* starts up normally using whatever control information has been specified in its run-control file. If a daemon is running, on the other hand, the new *fetchmail* instance just signals the old one to wake up and collect mail immediately; then the new instance terminates. In addition, **fetchmail -q** sends a termination signal to any running *fetchmail* daemon.

Thus, typing **fetchmail** means, in effect, "poll now and leave a daemon running to poll later; don\'t bother me with the detail of whether a daemon was already running or not". Observe that the detail of which particular signals are used for wakeup and termination is something the user doesn\'t have to know.
:::::

:::::::::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#sockets}Sockets {#sockets .title}

</div>
::::

Sockets[]{#id2922795 .indexterm} were developed in the BSD[]{#id2922804 .indexterm} lineage of Unix as a way to encapsulate access to data networks. Two programs communicating over a socket typically see a bidirectional byte stream (there are other socket modes and transmission methods, but they are of only minor importance). The byte stream is both sequenced (that is, even single bytes will be received in the same order sent) and reliable (socket users are guaranteed that the underlying network will do error detection and retry to ensure delivery). Socket descriptors, once obtained, behave essentially like file descriptors.

::: blockquote
  ---------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                         Sockets differ from read/write in one important case. If the bytes you send arrive, but the receiving machine fails to ACK, the sending machine\'s TCP/IP stack will time out. So getting an error does [*not*]{.emphasis} necessarily mean that the bytes didn\'t arrive; the receiver may be using them. This problem has profound consequences for the design of reliable protocols, because you have to be able to work properly when you don\'t know what was received in the past. Local I/O is 'yes/no'. Socket I/O is 'yes/no/maybe'. And nothing can ensure delivery --- the remote machine might have been destroyed by a comet.    
  \--[ [Ken Arnold]{.author} []{#id2922838 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
  ---------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

At the time a socket is created, you specify a [*protocol family*]{.emphasis} which tells the network layer how the name of the socket is interpreted. Sockets are usually thought of in connection with the Internet, as a way of passing data between programs running on different hosts; this is the AF_INET socket family, in which addresses are interpreted as host-address and service-number pairs. However, the AF_UNIX (aka AF_LOCAL) protocol family supports the same socket abstraction for communication between two processes on the same machine (names are interpreted as the locations of special files analogous to bidirectional named pipes). As an example, client programs and servers using the X windowing system[]{#id2922889 .indexterm} typically use AF_LOCAL sockets to communicate.

All modern Unixes support BSD-style []{#id2922903 .indexterm} sockets, and as a matter of design they are usually the right thing to use for bidirectional IPC no matter where your cooperating processes are located. Performance pressure may push you to use shared memory or tempfiles or other techniques that make stronger locality assumptions, but under modern conditions it is best to assume that your code will need to be scaled up to distributed operation. More importantly, those locality assumptions may mean that portions of your system get chummier with each others\' internals than ought to be the case in a good design. The separation of address spaces that sockets enforce is a feature, not a bug.

To use sockets gracefully, in the Unix tradition, start by designing an [*application protocol*]{.emphasis} for use between them --- a set of requests and responses which expresses the semantics of what your programs will be communicating about in a succinct way. We\'ve already discussed the some major issues in the design of application protocols in [Chapter 5](textualitychapter.html "Chapter 5. Textuality").

Sockets are supported in all recent Unixes, under Windows, and under classic MacOS as well.

::::: {.sect4 lang="en"}
:::: titlepage
<div>

##### []{#id2922950}Case Study: PostgreSQL {#case-study-postgresql .title}

</div>
::::

PostgreSQL is an open-source database program. Had it been implemented as a monster monolith, it would be a single program with an interactive interface that manipulates database files on disk directly. Interface would be welded together with implementation, and two instances of the program attempting to manipulate the same database at the same time would have serious contention and locking issues.

Instead, the PostgreSQL suite includes a server called *postmaster* and at least three client applications. One *postmaster* server process per machine runs in background and has exclusive access to the database files. It accepts requests in the SQL query minilanguage through TCP/IP[]{#id2922989 .indexterm} sockets, and returns answers in a textual format as well. When the user runs a PostgreSQL client, that client opens a session to *postmaster* and does SQL transactions with it. The server can handle several client sessions at once, and sequences requests so that they don\'t interfere with each other.

Because the front end and back end are separate, the server doesn\'t need to know anything except how to interpret SQL requests from a client and send SQL reports back to it. The clients, on the other hand, don\'t need to know anything about how the database is stored. Clients can be specialized for different needs and have different user interfaces.

This organization is quite typical for Unix databases --- so much so that it is often possible to mix and match SQL clients and SQL servers. The interoperability issues are the SQL server\'s TCP/IP[]{#id2923028 .indexterm} port number, and whether client and server support the same dialect of SQL.
:::::

::::: {.sect4 lang="en"}
:::: titlepage
<div>

##### []{#id2923040}Case Study: Freeciv {#case-study-freeciv .title}

</div>
::::

In [Chapter 6](transparencychapter.html "Chapter 6. Transparency"), we introduced Freeciv as an example of transparent data formats. But more critical to the way it supports multiplayer gaming is the client/server partitioning of the code. This is a representative example of a program in which the application needs to be distributed over a wide-area network and handles communication through TCP/IP sockets.

The state of a running Freeciv game is maintained by a server process, the game engine. Players run GUI clients which exchange information and commands with the server through a packet protocol. All game logic is handled in the server. The details of GUI are handled in the client; different clients support different interface styles.

This is a very typical organization for a multiplayer online game. The packet protocol uses TCP/IP[]{#id2923080 .indexterm} as a transport, so one server can handle clients running on different Internet hosts. Other games that are more like real-time simulations (notably first-person shooters) use raw Internet datagram protocol (UDP) and trade lower latency for some uncertainty about whether any given packet will be delivered. In such games, users tend to be issuing control actions continuously, so sporadic dropouts are tolerable, but lag is fatal.
:::::
::::::::::::

::::: {.sect3 lang="en"}
:::: titlepage
<div>

#### []{#id2923100}Shared Memory {#shared-memory .title}

</div>
::::

Whereas two processes using sockets to communicate may live on different machines (and, in fact, be separated by an Internet connection spanning half the globe), shared memory requires producers and consumers to be co-resident on the same hardware. But, if your communicating processes can get access to the same physical memory, shared memory will be the fastest way to pass information between them.

Shared memory may be disguised under different APIs, but on modern Unixes the implementation normally depends on the use of mmap(2) to map files into memory that can be shared between processes. POSIX[]{#id2923132 .indexterm} defines a shm_open(3) facility with an API that supports using files as shared memory; this is mostly a hint to the operating system that it need not flush the pseudofile data to disk.

Because access to shared memory is not automatically serialized by a discipline resembling read and write calls, programs doing the sharing must handle contention and deadlock issues themselves, typically by using semaphore variables located in the shared segment. The issues here resemble those in multithreading (see the end of this chapter for discussion) but are more manageable because default is [*not*]{.emphasis} to share memory. Thus, problems are better contained.

On systems where it is available and reliable, the Apache[]{#id2923174 .indexterm} web server\'s scoreboard facility uses shared memory for communication between an Apache master process and the load-sharing pool of Apache images that it manages. Modern X implementations also use shared memory, to pass large images between client and server when they are resident on the same machine, to avoid the overhead of socket communication. Both uses are performance hacks justified by experience and testing, rather than being architectural choices.

The mmap(2) call is supported under all modern Unixes, including Linux[]{#id2923205 .indexterm} and the open-source BSD []{#id2923214 .indexterm} versions; this is described in the Single Unix Specification. It will not normally be available under Windows, MacOS classic, and other operating systems.

Before purpose-built mmap(2) was available, a common way for two processes to communicate was for them to open the same file, and then delete that file. The file wouldn\'t go away until all open filehandles were closed, but some old Unixes took the link count falling to zero as a hint that they could stop updating the on-disk copy of the file. The downside was that your backing store was the file system rather than a swap device, the file system the deleted file lived on couldn\'t be unmounted until the programs using it closed, and attaching new processes to an existing shared memory segment faked up in this way was tricky at best.

After Version 7 and the split between the BSD[]{#id2923258 .indexterm} and System V[]{#id2923266 .indexterm} lineages, the evolution of Unix interprocess communication took two different directions. The BSD direction led to [sockets](ch07s02.html#sockets "Sockets"). The AT&T lineage, on the other hand, developed named pipes (as [previously discussed](ch07s02.html#named_pipes)) and an IPC facility, specifically designed for passing binary data and based on shared-memory bidirectional message queues. This is called 'System V IPC'---or, among old timers, 'Indian Hill' IPC after the AT&T facility where it was first written.

The upper, message-passing layer of System V IPC has largely fallen out of use. The lower layer, which consists of shared memory and semaphores, still has significant applications under circumstances in which one needs to do mutual-exclusion locking and some global data sharing among processes running on the same machine. These System V shared memory facilities evolved into the POSIX shared-memory API, supported under Linux, the BSDs, MacOS X and Windows, but not classic MacOS.

By using these shared-memory and semaphore facilities (shmget(2), semget(2), and friends) one can avoid the overhead of copying data through the network stack. Large commercial databases (including Oracle, DB2, Sybase, and Informix) use this technique heavily.
:::::
:::::::::::::::::::::::::::::::

::::::::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[68](ch07s02.html#id2915505){#ftn.id2915505}\]^ A common error in programming shellouts is to forget to block signals in the parent while the subprocess runs. Without this precaution, an interrupt typed to the subprocess can have unwanted side effects on the parent process.
:::

::: footnote
^\[[69](ch07s02.html#id2915659){#ftn.id2915659}\]^ Actually, the above is a slight oversimplification. See the discussion of `EDITOR` and `VISUAL` in [Chapter 10](configurationchapter.html "Chapter 10. Configuration") for the rest of the story.
:::

::: footnote
^\[[70](ch07s02.html#id2916197){#ftn.id2916197}\]^ The less(1) man page explains the name by observing "Less is more".
:::

::: footnote
^\[[71](ch07s02.html#id2921610){#ftn.id2921610}\]^ A common error is to use `$*` rather than "`$@`". This does bad things when handed a filename with embedded spaces.
:::

::: footnote
^\[[72](ch07s02.html#id2921897){#ftn.id2921897}\]^ *qmail-popup*\'s standard input and standard output are the socket, and standard error (which will be file descriptor 2) goes to a log file. File descriptor 3 is guaranteed to be the next to be allocated. As an infamous kernel comment once observed: "You are not expected to understand this".
:::

::: footnote
^\[[73](ch07s02.html#id2922127){#ftn.id2922127}\]^ The friend who suggested this case study comments: "Yes, you can get away with this technique\...if there are just a few easily-recognizable nuggets of information coming back from the slave process, and you have tongs and a radiation suit".
:::

::: footnote
^\[[74](ch07s02.html#id2922208){#ftn.id2922208}\]^ A particularly nasty variant of this attack is to drop in a named Unix-domain socket where the producer and consumer programs are expecting the tempfile to be.
:::

::: footnote
^\[[75](ch07s02.html#id2922479){#ftn.id2922479}\]^ A 'race condition' is a class of problem in which correct behavior of the system relies on two independent events happening in the right order, but there is no mechanism for ensuring that they actually will. Race conditions produce intermittent, timing-dependent problems that can be devilishly difficult to debug.
:::
:::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------------------------- ----------------------------------------------- --------------------------------------
  [Prev](ch07s01.html){accesskey="p"}                       [Up](multiprogramchapter.html){accesskey="u"}     [Next](ch07s03.html){accesskey="n"}
  Separating Complexity Control from Performance Tuning           [Home](index.html){accesskey="h"}                 Problems and Methods to Avoid
  -------------------------------------------------------- ----------------------------------------------- --------------------------------------
:::
