::: navheader
  The Right Size for an Editor                                    
  -------------------------------------- ------------------------ --------------------------------------
  [Prev](ch13s02.html){accesskey="p"}     Chapter 13. Complexity     [Next](ch13s04.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::::::::::::: {.sect1 lang="en"}
:::: titlepage
<div>

## []{#id2967255}The Right Size for an Editor {#the-right-size-for-an-editor .title style="clear: both"}

</div>
::::

Now let us examine our case studies using the complexity categories we developed at the beginning of this chapter.

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2967267}Identifying the Complexity Problems {#identifying-the-complexity-problems .title}

</div>
::::

Every text editor has a certain amount of essential complexity. At minimum, it has to maintain an internal buffer copy of the file or files the user is editing. Functions to import and export file data are a minimum requirement (usually from and to disk, though the stream editor sed(1) is an interesting exception). Some way to modify the buffer must be supported, though we cannot specify what way without describing specific features that are optional. Our four examples show widely varying levels of optional and accidental complexity beyond this.

Of all of these, ed(1) has the least complexity. Almost the only non-orthogonal feature in its command set is the fact that many of its commands can take a 'p' or 'l' suffix to print or list command results. Even after three decades of feature additions there are fewer than thirty editing commands, and the normal working set for most users will be less than a dozen. There is not much in the way of optional complexity that could be removed here, and it\'s hard to identify any accidental complexity at all. The user interface of ed is strictly compact.

On the flip side, the ed interface is not really suitable for editing tasks even as basic as rapidly flipping through a text file. One has to limit one\'s objectives pretty sharply for ed to become an acceptable solution for interactive editing.

Suppose, then, that we add "support visual browsing and editing of multiple files" as an objective? Then Sam seems not very far from being the minimal ed extension that could achieve this. The fact that the designers did not change the semantics of the inherited ed commands is notable; they kept an existing, orthogonal set and added a relatively small set of capabilities that are themselves orthogonal.

One large increase in optional (implementation) complexity is Sam\'s infinite-undo capability. Another significant one is the new regular-expression-based loop and iteration facility in the command language. These, and the fact that the mouse can be used as a selection device, are about all that distinguish Sam from a hypothetical ed with a mouse-and-windows interface.

Without a thorough code audit it\'s difficult to be sure, but at the design level it\'s hard to identify any accidental complexity in Sam. The interface is at least semi-compact and arguably strictly compact. This editor lives up to the very highest standards of Unix design --- unsurprisingly, given its provenance.

By contrast, vi looks rather bloated and flabby. There are hundreds of commands, many of them duplicative. These are at best optional complexity, and perhaps accidental. At a guess, most users don\'t know more than 5% of the command set. With the example of Sam before us, it\'s fair to wonder why the interface complexity of vi is so high.

In [Chapter 11](interfacechapter.html "Chapter 11. Interfaces") we described the effect of the absence of standard arrow keys on early roguelike programs; vi was one of these. When vi was built, its author knew that many of his users would need to be able to use the cursor motion keys traditional on Unix glass teletypes. This made a modal interface inevitable. Once the hjkl keys had mode-dependent meanings in an edit buffer, it was all too easy to fall into the habit of adding new commands in an ad-hoc way.

Sam, designed as it is to depend on a bitmapped display with both arrow keys and a mouse, can be much cleaner. And it is.

But the clutter of vi commands is a relatively superficial problem. It\'s interface complexity, yes, but of a kind most users can and do ignore (the interface is semi-compact in the sense we developed in [Chapter 4](modularitychapter.html "Chapter 4. Modularity")). The deeper problem is an adhocity trap. Over the years, vi has had progressively more and more special-purpose C code bolted onto it to perform tasks that Sam refuses to do and that Emacs would attack with Lisp code modules and subprocess control. The extensions are not, as in Emacs, libraries loaded as needed; users pay the overhead for the resulting code bloat all the time. As a result, the size difference between a modern vi and a modern Emacs is not nearly as great as one might expect; in mid-2003 on an Intel-architecture machine, it\'s 1500KB for GNU Emacs versus 900KB for vim. There is a whole lot of both optional and accidental complexity in that 900KB.

For vi partisans, not having an embedded scripting language --- not being Emacs --- has become an identity issue, a central part of the shared myth that vi is a lightweight editor. While vi fans like to talk about filtering buffers with external programs and scripts to do what Emacs\'s embedded scripting does, the reality is that vi\'s "!" command cannot filter regions of an edit buffer selected at finer granularity than a range of lines (Sam and Wily, though they have no more subprocess management than vi does, can at least filter arbitrary text ranges, not just line ranges). All knowledge of file formats and syntaxes that vary at a finer granularity (and most do) has to be built in to C code if vi is going to have it available at all. There is thus little prospect that the codebase-size ratio between Emacs and vi will improve in favor of vi; indeed, it seems likely to get worse.

Emacs is sufficiently large, and has a sufficiently tangled history, to make separating its optional from its accidental complexity quite a challenge. We can at least begin by trying to separate the dispensable accidents of the Emacs design from its indispensable essentials.

Perhaps the most conspicuously dispensable part of the Emacs design is Emacs Lisp[]{#id2967467 .indexterm}. It is essential to what Emacs does that it features what we nowadays call an embedded scripting language, but Emacs would be little different in capability if that language had been Python or Java or Perl. At the time Emacs was designed in the 1970s, however, Lisp was about the only language that had the characteristics (including unlimited-extent types and garbage collection) to fit it to the job.

Much in the particulars of the way *emacs* handles event processing and drives a bitmapped display (including the support for internationalization) is accidental as well. The one great schism in its history (the GNU Emacs/XEmacs fork) was over these issues, and demonstrates that nothing in the rest of the design prefers or requires any one event model.

On the other hand, the ability to bind arbitrary event sequences to arbitrary built-in or user-defined functions is indispensable. The scripting language could change and the event model could change, but without the anything-goes polymorphism in the way they are connected, the Emacs design would be both unrecognizable and crippled. Extension modes would have to fight each other for ownership of a limited event set, and activating multiple cooperating modes on the same buffer would be difficult or impossible.

The huge library of extension modes shipped with Emacs is accidental as well. The [*ability*]{.emphasis} to construct such extensions may be essential, but the particular set we have is a product of history and chance. They could all be different or replaced; the result would still, recognizably, be Emacs.

But subprocess interaction is indispensable. Without it, Emacs modes could not perform the expected IDE-like integration and front-ending of many different tools.

Experience with small editors that clone the default keybindings and appearance of Emacs without emulating its extensibility is instructive. There have been several such clones, of which the best known are probably *MicroEmacs* and *pico*, but none have ever acquired significant mindshare.

Having identified accident and essence in the Emacs design helps us get a handle on which of its complexity is optional and which accidental. But, more importantly, they help us see past the superficial differences between Emacs and the previous three editors we have considered, to the really critical difference: the fact that the objectives of the Emacs design are far more broad. Emacs wants to be a unified interface to all tools that operate on text.

Wily makes an interesting contrast with Emacs. As with Sam, the amount of optional complexity is low; the Wily user interface can be succinctly but effectively described in a single page.

But this elegance comes with a price; it is not possible to bind functions to any keystrokes or input gestures other than a restricted set of mouse chords. Instead, every editor function other than very basic text insertion and deletion has to be implemented with a program outboard of the editor, either a standalone script or a specialized symbiont process listening to Wily input events. (The former technique relies on outboard program startups being fast enough not to produce noticeable interface lag, something which was emphatically not the case in either Emacs\'s natal environment or under the Unixes it was first ported to.)

Optional complexity which Emacs would implement in Lisp extension modes is instead distributed through specialized symbionts; each has to know the special Wily messaging interface. An advantage of this approach is that such symbionts can be written in any language the user chooses. In addition, the symbionts (because they run outboard) cannot adversely affect each other or the Wily core (which is not true of Emacs modes). A disadvantage is that Wily itself cannot directly do subprocess interaction with ordinary Unix tools at all.

In this and other ways, *wily\'s* distributed scripting is not as powerful as the embedded scripting of Emacs. The scope of Wily\'s objectives is correspondingly narrower; the authors disclaim any interest in syntax-aware editing, or rich text, for example, and neither Wily nor its Plan 9 ancestor *acme* can do these things.

This brings us to another, and sharper way of posing the central question of this chapter: When do large objectives justify a large program?
:::::

::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2967642}Compromise Doesn\'t Work {#compromise-doesnt-work .title}

</div>
::::

The comparison between Sam and vi suggests strongly that, at least where editors are concerned, attempts to compromise between the minimalism of ed and the all-singing-all-dancing comprehensiveness of Emacs don\'t work very well; vi attempts this, and ends up with neither virtue. Instead, it falls into an adhocity trap. Wily avoids the adhocity trap, but cannot match the power of Emacs and must demand a custom process interface from each of its interactive symbionts in order to come anywhere close.

Evidently something about editors tends to push them in the direction of increasing complexity. In the case of vi, that something is not hard to identify; it\'s the desire for convenience. While ed may be theoretically adequate, very few people (other than perhaps Ken Thompson himself) would forgo screen-oriented editing to make a statement about software bloat.

More generally, programs that mediate between the user and the rest of the universe notoriously attract features. This includes not just editors but Web browsers, mail and newsgroup readers, and other communications programs. All tend to evolve in accordance with the Law of Software Envelopment, aka Zawinski\'s Law: "Every program attempts to expand until it can read mail. Those programs which cannot so expand are replaced by ones which can".

Jamie Zawinski, inventor of the Law (and one of the principal authors of the Netscape and Mozilla Web browsers), maintains more generally that all really useful programs tend to turn into Swiss Army knives. The commercial success of large, integrated application suites outside the Unix world tends to confirm this, and directly challenges the Unix philosophy of minimalism.

To the extent Zawinski\'s Law is correct, it suggests that some things want to be small and some want to be large, but the middle ground is unstable. The superficial problems with vi can be put down to history, but the deeper ones trace back to the combination of steady pressure to add features with refusal to embed the scripting and subprocess-control features that vi partisans associate with excessive size. On a different level, accepting that there would be two modes in the interface (insertion versus character-motion) opened a can of worms --- it became far too easy to add new commands without thinking about their complexity impact on the overall design.

The examples of Emacs and Wily further suggest [*why*]{.emphasis} some things want to be large: so that several related tasks can share context. Editing and version control (or editing and mail, editing and symbolic debugging, etc.) are separate tasks from the point of view of the implementers --- but users would often prefer to have one big environment that lets them point at pieces of text, rather than spend time and attention ping-ponging between several programs that each have to have the same filename or the contents of some cut buffer handed to them.

More generally, let\'s suppose we view the entire Unix environment as a single work of design by community. Then the religion of "small, sharp tools", the pressure to keep interface complexity and codebase size down, may lead right to a manularity trap --- the user has to maintain all the shared context himself, because the tools won\'t do it for him.

Returning to the specific context of editors, Sam shows us that vi is the wrong thing. Wily is a valiant effort to avoid the vastness of Emacs that falls short because it can\'t be syntax-aware. But Wily, or some realization of the Emacs design ideas cleaned up and stripped of historical baggage, might be the right thing. The value of optional complexity depends on the objectives you choose, and the ability to share context among all the text-oriented tools related to a task is valuable.
:::::

::::::: {.sect2 lang="en"}
:::: titlepage
<div>

### []{#id2967765}Is Emacs an Argument against the Unix Tradition? {#is-emacs-an-argument-against-the-unix-tradition .title}

</div>
::::

The traditional Unix view of the world, however, is so attached to minimalism that it isn\'t very good at distinguishing between the adhocity-trap problems of vi and the optional complexity of Emacs.

::: blockquote
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                           The reason that vi and emacs never caught on among old-school Unix programmers is that they are [*ugly*]{.emphasis}. This complaint may be "old Unix" speaking, but had it not been for the singular taste of old Unix, "new Unix" would not exist.    
  \--[ [Doug McIlroy]{.author} []{#id2967793 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                          
  ------------------------------------------------------------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Attacks on Emacs by vi users --- along with attacks on vi by the hard-core old-school types still attached to ed --- are episodes in a larger argument, a contest between the exuberance of wealth and the virtues of austerity. This argument correlates with the tension between the old-school and new-school styles of Unix.

The "singular taste of old Unix" was partly a consequence of poverty in exactly the same way that Japanese minimalism was --- one learns to do more with less most effectively when having more is not an option. But Emacs (and new-school Unix, reinvented on powerful PCs and fast networks) is a child of wealth.

::: blockquote
  ------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
                                                                           As, in a different way, was old-school Unix. Bell Labs had enough resources so that Ken was not confined by demands to have a product yesterday. Recall Pascal\'s apology for writing a long letter because he didn\'t have enough time to write a short one.    
  \--[ [Doug McIlroy]{.author} []{#id2967862 .indexterm} ]{.attribution}                                                                                                                                                                                                                                                                    
  ------------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ---
:::

Ever since, Unix programmers have maintained a tradition that exalts the elegant over the excessive.

The vastness of Emacs, on the other hand, did not originate under Unix, but was invented by Richard M. Stallman[]{#id2967893 .indexterm} within a very different culture that flourished at the MIT Artificial Intelligence Lab in the 1970s. The MIT AI lab was one of the wealthiest corners of computer-science academia; people learned to treat computing resources as cheap, anticipating an attitude that would not be viable elsewhere until fifteen years later. Stallman was unconcerned with minimalism; he sought the maximum power and scope for his code.

The central tension in the Unix tradition has always been between doing more with less and doing more with more. It recurs in a lot of different contexts, often as a struggle between designs that have the quality of clean minimalism and others that choose expressive range and power even at the cost of high complexity. For both sides, the arguments for or against Emacs have exemplified this tension since it was first ported to Unix in the early 1980s.

Programs that are both as useful and as large as Emacs make Unix programmers uncomfortable precisely because they force us to face the tension. They suggest that old-school Unix minimalism is valuable as a discipline, but that we may have fallen into the error of dogmatism.

There are two ways Unix programmers can address this problem. One is to deny that large is actually large. The other is to develop a way of thinking about complexity that is not a dogma.

Our thought experiment with replacing Lisp and the extension libraries gives us a new perspective on the oft-heard charge that Emacs is bloated because its extension library is so large. Perhaps this is as unfair as charging that */bin/sh* is bloated because the collection of all shellscripts on a system is large. Emacs could be considered a virtual machine or framework around a collection of small, sharp tools (the modes) that happen to be written in Lisp[]{#id2967958 .indexterm}.

On this view, the main difference between the shell and Emacs is that Unix distributors don\'t ship all the world\'s shellscripts along with the shell. Objecting to Emacs because having a general-purpose language in it feels like bloat is approximately as silly as refusing to use shellscripts because shell has conditionals and for loops. Just as one doesn\'t have to learn shell to use shellscripts, one doesn\'t have to learn Lisp to use Emacs. If Emacs has a design problem, it\'s not so much the Lisp interpreter (the framework part) as the fact that the mode library is an untidy heap of historical accretions --- but that\'s a source of complexity users can ignore, because they won\'t be affected by what they don\'t use.

This mode of argument is very comforting. It can be applied to other tool-integration frameworks, such as the (uncomfortably large) GNOME and KDE desktop projects. There is some force to it. And yet, we should be suspicious of any 'perspective' that offers to resolve all our doubts so neatly; it might be a rationalization, not a rationale.

Therefore, let\'s avoid the possibility of falling into denial and accept that Emacs is both useful and large --- that it [*is*]{.emphasis} an argument against Unix minimalism. What does our analysis of the kinds of complexity in it, and the motives for it, suggest beyond that? And is there reason to believe that those lessons generalize?
:::::::
::::::::::::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- --------------------------------------------- --------------------------------------
  [Prev](ch13s02.html){accesskey="p"}     [Up](complexitychapter.html){accesskey="u"}     [Next](ch13s04.html){accesskey="n"}
  A Tale of Five Editors                       [Home](index.html){accesskey="h"}                   The Right Size of Software
  -------------------------------------- --------------------------------------------- --------------------------------------
:::
