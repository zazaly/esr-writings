::: navheader
  The Importance of Being Textual                                          
  ------------------------------------------------ ----------------------- --------------------------------------
  [Prev](textualitychapter.html){accesskey="p"}     Chapter 5. Textuality     [Next](ch05s02.html){accesskey="n"}

------------------------------------------------------------------------
:::

::::::::::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2906458}The Importance of Being Textual {#the-importance-of-being-textual .title style="clear: both"}

</div>
::::

Pipes and sockets will pass binary data as well as text. But there are good reasons the examples we\'ll see in [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming") are textual: reasons that hark back to Doug McIlroy\'s[]{#id2906475 .indexterm} advice quoted in [Chapter 1](philosophychapter.html "Chapter 1. Philosophy"). Text streams are a valuable universal format because they\'re easy for human beings to read, write, and edit without specialized tools. These formats are (or can be designed to be) transparent.

Also, the very limitations of text streams help enforce encapsulation. By discouraging elaborate representations with rich, densely encoded structure, text streams also discourage programs from being promiscuous with each other about their internal states and help enforce encapsulation. We\'ll return to this point at the end of [Chapter 7](multiprogramchapter.html "Chapter 7. Multiprogramming") when we discuss RPC.

When you feel the urge to design a complex binary file format, or a complex binary application protocol, it is generally wise to lie down until the feeling passes. If performance is what you\'re worried about, implementing compression on the text protocol stream either at some level below or above the application protocol will give you a cleaner and perhaps better-performing design than a binary protocol (text compresses well, and quickly).

::: blockquote
  ------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                            A bad example of binary formats in Unix history was the way device-independent *troff* read a binary file containing device information, supposedly for speed. The initial implementation generated that binary file from a text description in a somewhat unportable way. Faced with a need to port *ditroff* [*quickly*]{.emphasis} to a new machine, rather than reinvent the binary goo, I ripped it out and just had *ditroff* read the text file. With carefully crafted file-reading code, the speed penalty was negligible.    
  \--[ [Henry Spencer]{.author} []{#id2901108 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
  ------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Designing a textual protocol tends to future-proof your system. One specific reason is that ranges on numeric fields aren\'t implied by the format itself. Binary formats usually specify the number of bits allocated to a given value, and extending them is difficult. For example, IPv4 only allows 32 bits for an address. To extend address size to 128 bits (as done by IPv6) requires a major revamping.^\[[51](ch05s01.html#ftn.id2901165){#id2901165}\]^ In contrast, if you need a larger value in a text format, just write it. It may be that a given program can\'t receive values in that range, but it\'s usually easier to modify the program than to modify all the data stored in that format.

The only good justification for a binary protocol is if you\'re going to be manipulating large enough data sets that you\'re genuinely worried about getting the most bit-density out of your media, or if you\'re very concerned about the time or instruction budget required to interpret the data into an in-core structure. Formats for large images and multimedia are sometimes an example of the former, and network protocols with hard latency requirements sometimes an example of the latter.

::: blockquote
  ---------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                         The reciprocal problem with SMTP or HTTP-like text protocols is that they tend to be expensive in bandwidth and slow to parse. The smallest X request is 4 bytes: the smallest HTTP request is about 100 bytes. X requests, including amortized overhead of transport, can be executed in the order of 100 instructions; at one point, an Apache[]{#id2901227 .indexterm} \[web server\] developer proudly indicated they were down to 7000 instructions. For graphics, bandwidth becomes everything on output; hardware is designed such that these days the graphics-card bus is [*the*]{.emphasis} bottleneck for small operations, so any protocol had better be very tight if it is not to be a worse bottleneck. This is the extreme case.    
  \--[ [Jim Gettys]{.author} []{#id2901209 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       
  ---------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

These concerns are valid in other extreme cases as well as in X --- for example, in the design of graphics file formats intended to hold very large images. But they are usually just another case of premature-optimization[]{#id2901256 .indexterm} fever. Textual formats don\'t necessarily have much lower bit density than binary ones; they do after all use seven out of eight bits per byte. And what you gain by not having to parse text, you generally lose the first time you need to generate a test load, or to eyeball a program-generated example of your format and figure out what\'s in there.

In addition, the kind of thinking that goes into designing tight binary formats tends to fall down on making them cleanly extensible. The X designers experienced this:

::: blockquote
  ---------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                         Against the current X framework is the fact we didn\'t design enough of a structure to make it easier to ignore trivial extensions to the protocol; we can do this some of the time, but a bit better framework would have been good.    
  \--[ [Jim Gettys]{.author} []{#id2901296 .indexterm} ]{.attribution}                                                                                                                                                                                                                                            
  ---------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

When you think you have an extreme case that justifies a binary file format or protocol, you need to think very carefully about extensibility[]{#id2901321 .indexterm} and leaving room in the design for growth.

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2901332}Case Study: Unix Password File Format {#case-study-unix-password-file-format .title}

</div>
::::

On many operating systems, the per-user data required to validate logins and start a user\'s session is an opaque binary database. Under Unix, by contrast, it\'s a text file with records one per line and colon-separated fields.

[Example 5.1](ch05s01.html#passwd "Example 5.1. Password file example.") consists of some randomly-chosen example lines:

::: example
[]{#passwd}

**Example 5.1. Password file example.**

``` programlisting
games:*:12:100:games:/usr/games:
gopher:*:13:30:gopher:/usr/lib/gopher-data:
ftp:*:14:50:FTP User:/home/ftp:
esr:0SmFuPnH5JlNs:23:23:Eric S. Raymond:/home/esr:
nobody:*:99:99:Nobody:/:
```
:::

Without even knowing anything about the semantics of the fields, we can notice that it would be hard to pack the data much tighter in a binary format. The colon sentinel characters would have to have functional equivalents taking at least as much space (usually either count bytes or NULs). The per-user records would either have to have terminators (which could hardly be shorter than a single newline) or else be wastefully padded out to a fixed length.

Actually the prospects for saving space through binary encoding pretty much vanish if you know the actual semantics of the data. The numeric user ID (3rd) and group ID (4th) fields are integers, thus on most machines a binary representation would be at least 4 bytes, and longer than the text for values up to 999. But let\'s agree to ignore this for now and suppose the best case that the numeric fields have a 0-255 range.

We could tighten up the numeric fields (3rd and 4th) by collapsing the numerics to single bytes, and the password strings (2nd) to an 8-bit encoding. On this example, that would give about an 8% size decrease.

That 8% of putative inefficiency buys us a lot. It avoids putting an arbitrary limit on the range of the numeric fields. It gives us the ability to modify the password file with any old text editor of our choice, rather than having to build a specialized tool to edit a binary format (though in the case of the password file itself, we have to be extra careful about concurrent edits). And it gives us the ability to do ad-hoc searches and filters and reports on the user account information with text-stream tools such as grep(1).

We do have to be a bit careful about not embedding a colon in any of the textual fields. Good practice is to tell the file write code to precede embedded colons with an escape character, and then to tell the file read code to interpret it. Unix tradition favors backslash for this use.

The fact that structural information is conveyed by field position rather than an explicit tag makes this format faster to read and write, but a bit rigid. If the set of properties associated with a key is expected to change with any frequency, one of the tagged formats described below might be a better choice.

Economy is not a major issue with password files to begin with, as they\'re normally read seldom^\[[52](ch05s01.html#ftn.id2901458){#id2901458}\]^ and infrequently modified. Interoperability is not an issue, since various data in the file (notably user and group numbers) are not portable off the originating machine. For password files, it\'s therefore quite clear that going where the transparency criterion[]{#id2901480 .indexterm} leads was the right thing.
::::::

:::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2901494}Case Study: `.newsrc` Format {#case-study-.newsrc-format .title}

</div>
::::

Usenet[]{#id2901510 .indexterm} news is a worldwide distributed bulletin-board system that anticipated today\'s P2P networking by two decades. It uses a message format very similar to that of RFC 822 electronic-mail messages, except that instead of being directed to personal recipients messages are sent to topic groups. Articles posted at any participating site are broadcast to each site that it has registered as a neighbor, and eventually flood-fill to all news sites.

Almost all Usenet news readers understand the `.newsrc` file, which records which Usenet messages have been seen by the calling user. Though it is named like a run-control file, it is not only read at startup but typically updated at the end of the newsreader run. The `.newsrc` format has been fixed since the first newsreaders around 1980. [Example 5.2](ch05s01.html#newsrc "Example 5.2. A .newsrc example.") is a representative section from a `.newsrc` file.

::: example
[]{#newsrc}

**Example 5.2. A `.newsrc` example.**

``` programlisting
rec.arts.sf.misc! 1-14774,14786,14789
rec.arts.sf.reviews! 1-2534
rec.arts.sf.written: 1-876513
news.answers! 1-199359,213516,215735
news.announce.newusers! 1-4399
news.newusers.questions! 1-645661
news.groups.questions! 1-32676
news.software.readers! 1-95504,137265,137274,140059,140091,140117
alt.test! 1-1441498
```
:::

Each line sets properties for the newsgroup named in the first field. The name is immediately followed by a character that indicates whether the owning user is currently subscribed to the group or not; a colon indicates subscription, and an exclamation mark indicates nonsubscription. The remainder of the line is a sequence of comma-separated article numbers or ranges of article numbers, indicating which articles the user has seen.

Non-Unix programmers might have automatically tried to design a fast binary format in which each newsgroup status was described by either a long but fixed-length binary record, or a sequence of self-describing binary packets with internal length fields. The main point of such a binary representation would be to express ranges with binary data in paired word-length fields, in order to avoid the overhead of parsing all the range expressions at startup.

Such a layout could be read and written faster than a textual format, but it would have other problems. A naïve implementation in fixed-length records would have placed artificial length limits on newsgroup names and (more seriously) on the maximum number of ranges of seen-article numbers. A more sophisticated binary-packet format would avoid the length limits, but could not be edited with the user\'s eyeballs and fingers --- a capability that can be quite useful when you want to reset just some of the read bits in an individual newsgroup. Also, it would not necessarily be portable to different machine types.

The designers of the original newsreader chose transparency[]{#id2901641 .indexterm} and interoperability over economy. The case for going in the other direction was not completely ridiculous; `.newsrc` files can get very large, and one modern reader (GNOME\'s Pan) uses a speed-optimized private format to avoid startup lag. But to other implementers, textual representation looked like a good tradeoff in 1980, and has looked better as machines increased in speed and storage dropped in price.
::::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#png}Case Study: The PNG Graphics File Format {#case-study-the-png-graphics-file-format .title}

</div>
::::

[]{#id2901678 .indexterm}

PNG (Portable Network Graphics) is a file format for bitmap graphics.[]{#id2901693 .indexterm} It is like GIF, and unlike JPEG, in that it uses lossless compression and is optimized for applications such as line art and icons rather than photographic images. Documentation and open-source reference libraries of high quality are available at the [Portable Network Graphics website](http://www.libpng.org/pub/png/){target="_top"}.

PNG is an excellent example of a thoughtfully designed binary format. A binary format is appropriate since graphics files may contain very large amounts of data, such that storage size and Internet download time would go up significantly if the pixel data were stored textually. Transaction economy was the prime consideration, with transparency[]{#id2901724 .indexterm} sacrificed.^\[[53](ch05s01.html#ftn.id2901736){#id2901736}\]^ The designers were, however, careful about interoperability; PNG specifies byte orders, integer word lengths, endianness, and (lack of) padding between fields.

A PNG file consists of a sequence of chunks, each in a self-describing format beginning with the chunk type name and the chunk length. Because of this organization, PNG does not need a release number. New chunk types can be added at any time; the case of the first letter in the chunk type name informs PNG-using software whether or not each chunk can be safely ignored.

The PNG file header also repays study. It has been cleverly designed to make various common kinds of file corruption (e.g., by 7-bit transmission links, or mangling of CR and LF characters) easy to detect.

The PNG standard is precise, comprehensive, and well written. It could serve as a model for how to write file format standards.
:::::

:::::: footnotes
\

------------------------------------------------------------------------

::: footnote
^\[[51](ch05s01.html#id2901165){#ftn.id2901165}\]^ There is a legend that some early airline reservation systems allocated exactly one byte for a plane\'s passenger count. Supposedly they became very confused by the arrival of the Boeing 747, the first plane that could carry more than 255 passengers.
:::

::: footnote
^\[[52](ch05s01.html#id2901458){#ftn.id2901458}\]^ Password files are normally read once per user session at login time, and after that occasionally by file-system utilities like ls(1) that must map from numeric user and group IDs to names.
:::

::: footnote
^\[[53](ch05s01.html#id2901736){#ftn.id2901736}\]^ Confusingly, PNG supports a different kind of transparency --- transparent pixels in the PNG image.
:::
::::::
:::::::::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  ------------------------------------------------ --------------------------------------------- --------------------------------------
  [Prev](textualitychapter.html){accesskey="p"}     [Up](textualitychapter.html){accesskey="u"}     [Next](ch05s02.html){accesskey="n"}
  Chapter 5. Textuality                                  [Home](index.html){accesskey="h"}                        Data File Metaformats
  ------------------------------------------------ --------------------------------------------- --------------------------------------
:::
