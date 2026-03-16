::: navheader
  Part II. Design                            
  -------------------------------------- --- ------------------------------------------------
  [Prev](ch03s03.html){accesskey="p"}           [Next](modularitychapter.html){accesskey="n"}

------------------------------------------------------------------------
:::

:::::: {.part lang="en"}
:::: titlepage
<div>

# []{#design}Design {#design .title}

</div>
::::

::: toc
**Table of Contents**

4\. [Modularity](modularitychapter.html)

[Encapsulation and Optimal Module Size](ch04s01.html)

[Compactness and Orthogonality](ch04s02.html)

[Compactness](ch04s02.html#compactness)

[Orthogonality](ch04s02.html#orthogonality)

[The SPOT Rule](ch04s02.html#spot_rule)

[Compactness and the Strong Single Center](ch04s02.html#id2895445)

[The Value of Detachment](ch04s02.html#id2899405)

[Software Is a Many-Layered Thing](ch04s03.html)

[Top-Down versus Bottom-Up](ch04s03.html#id2899552)

[Glue Layers](ch04s03.html#id2899777)

[Case Study: C Considered as Thin Glue](ch04s03.html#c_thin_glue)

[Libraries](ch04s04.html)

[Case Study: GIMP Plugins](ch04s04.html#gimp_plugins)

[Unix and Object-Oriented Languages](unix_and_oo.html)

[Coding for Modularity](ch04s06.html)

5\. [Textuality](textualitychapter.html)

[The Importance of Being Textual](ch05s01.html)

[Case Study: Unix Password File Format](ch05s01.html#id2901332)

[Case Study: .newsrc Format](ch05s01.html#id2901494)

[Case Study: The PNG Graphics File Format](ch05s01.html#png)

[Data File Metaformats](ch05s02.html)

[DSV Style](ch05s02.html#id2901882)

[RFC 822 Format](ch05s02.html#id2902039)

[Cookie-Jar Format](ch05s02.html#id2902164)

[Record-Jar Format](ch05s02.html#id2906931)

[XML](ch05s02.html#id2907018)

[Windows INI Format](ch05s02.html#id2907263)

[Unix Textual File Format Conventions](ch05s02.html#id2907428)

[The Pros and Cons of File Compression](ch05s02.html#id2907903)

[Application Protocol Design](ch05s03.html)

[Case Study: SMTP, the Simple Mail Transfer Protocol](ch05s03.html#id2908194)

[Case Study: POP3, the Post Office Protocol](ch05s03.html#id2908383)

[Case Study: IMAP, the Internet Message Access Protocol](ch05s03.html#id2908582)

[Application Protocol Metaformats](ch05s04.html)

[The Classical Internet Application Metaprotocol](ch05s04.html#id2908835)

[HTTP as a Universal Application Protocol](ch05s04.html#id2908915)

[BEEP: Blocks Extensible Exchange Protocol](ch05s04.html#id2909217)

[XML-RPC, SOAP, and Jabber](ch05s04.html#id2909294)

6\. [Transparency](transparencychapter.html)

[Studying Cases](ch06s01.html)

[Case Study: audacity](ch06s01.html#audacity)

[Case Study: fetchmail\'s -v option](ch06s01.html#fetchmail_v)

[Case Study: GCC](ch06s01.html#id2909841)

[Case Study: kmail](ch06s01.html#id2909954)

[Case Study: SNG](ch06s01.html#id2910193)

[Case Study: The Terminfo Database](ch06s01.html#id2910334)

[Case Study: Freeciv Data Files](ch06s01.html#id2914115)

[Designing for Transparency and Discoverability](ch06s02.html)

[The Zen of Transparency](ch06s02.html#zen_of_transparency)

[Coding for Transparency and Discoverability](ch06s02.html#id2914509)

[Transparency and Avoiding Overprotectiveness](ch06s02.html#id2914680)

[Transparency and Editable Representations](ch06s02.html#id2914758)

[Transparency, Fault Diagnosis, and Fault Recovery](ch06s02.html#id2915107)

[Designing for Maintainability](ch06s03.html)

7\. [Multiprogramming](multiprogramchapter.html)

[Separating Complexity Control from Performance Tuning](ch07s01.html)

[Taxonomy of Unix IPC Methods](ch07s02.html)

[Handing off Tasks to Specialist Programs](ch07s02.html#id2915475)

[Pipes, Redirection, and Filters](ch07s02.html#plumbing)

[Wrappers](ch07s02.html#id2921506)

[Security Wrappers and Bernstein Chaining](ch07s02.html#id2921634)

[Slave Processes](ch07s02.html#id2922002)

[Peer-to-Peer Inter-Process Communication](ch07s02.html#id2922148)

[Problems and Methods to Avoid](ch07s03.html)

[Obsolescent Unix IPC Methods](ch07s03.html#id2923376)

[Remote Procedure Calls](ch07s03.html#id2923675)

[Threads --- Threat or Menace?](ch07s03.html#id2923889)

[Process Partitioning at the Design Level](ch07s04.html)

8\. [Minilanguages](minilanguageschapter.html)

[Understanding the Taxonomy of Languages](ch08s01.html)

[Applying Minilanguages](ch08s02.html)

[Case Study: sng](ch08s02.html#id2924747)

[Case Study: Regular Expressions](ch08s02.html#regexps)

[Case Study: Glade](ch08s02.html#id2933450)

[Case Study: m4](ch08s02.html#id2933775)

[Case Study: XSLT](ch08s02.html#id2934034)

[Case Study: The Documenter\'s Workbench Tools](ch08s02.html#id2934197)

[Case Study: fetchmail Run-Control Syntax](ch08s02.html#fetchmailrc)

[Case Study: awk](ch08s02.html#awk)

[Case Study: PostScript](ch08s02.html#id2935613)

[Case Study: bc and dc](ch08s02.html#id2935779)

[Case Study: Emacs Lisp](ch08s02.html#emacs_lisp_study)

[Case Study: JavaScript](ch08s02.html#javascript)

[Designing Minilanguages](ch08s03.html)

[Choosing the Right Complexity Level](ch08s03.html#id2936413)

[Extending and Embedding Languages](ch08s03.html#id2936650)

[Writing a Custom Grammar](ch08s03.html#id2936912)

[Macros --- Beware!](ch08s03.html#macroexpansion)

[Language or Application Protocol?](ch08s03.html#id2937424)

9\. [Generation](generationchapter.html)

[Data-Driven Programming](ch09s01.html)

[Case Study: ascii](ch09s01.html#id2939746)

[Case Study: Statistical Spam Filtering](ch09s01.html#bayes_spam)

[Case Study: Metaclass Hacking in fetchmailconf](ch09s01.html#fetchmailconf)

[Ad-hoc Code Generation](ch09s02.html)

[Case Study: Generating Code for the ascii Displays](ch09s02.html#id2938615)

[Case Study: Generating HTML Code for a Tabular List](ch09s02.html#htmlgen)

10\. [Configuration](configurationchapter.html)

[What Should Be Configurable?](ch10s01.html)

[Where Configurations Live](ch10s02.html)

[Run-Control Files](ch10s03.html)

[Case Study: The .netrc File](ch10s03.html#id2942210)

[Portability to Other Operating Systems](ch10s03.html#id2942358)

[Environment Variables](ch10s04.html)

[System Environment Variables](ch10s04.html#id2942463)

[User Environment Variables](ch10s04.html#id2942749)

[When to Use Environment Variables](ch10s04.html#id2942882)

[Portability to Other Operating Systems](ch10s04.html#id2947980)

[Command-Line Options](ch10s05.html)

[The -a to -z of Command-Line Options](ch10s05.html#id2948149)

[Portability to Other Operating Systems](ch10s05.html#id2950162)

[How to Choose among the Methods](ch10s06.html)

[Case Study: fetchmail](ch10s06.html#fetchmail_environment)

[Case Study: The XFree86 Server](ch10s06.html#id2950578)

[On Breaking These Rules](ch10s07.html)

11\. [Interfaces](interfacechapter.html)

[Applying the Rule of Least Surprise](ch11s01.html)

[History of Interface Design on Unix](ch11s02.html)

[Evaluating Interface Designs](ch11s03.html)

[Tradeoffs between CLI and Visual Interfaces](ch11s04.html)

[Case Study: Two Ways to Write a Calculator Program](ch11s04.html#id2951734)

[Transparency, Expressiveness, and Configurability](ch11s05.html)

[Unix Interface Design Patterns](ch11s06.html)

[The Filter Pattern](ch11s06.html#id2957637)

[The Cantrip Pattern](ch11s06.html#id2957916)

[The Source Pattern](ch11s06.html#id2958032)

[The Sink Pattern](ch11s06.html#id2958116)

[The Compiler Pattern](ch11s06.html#id2958199)

[The ed pattern](ch11s06.html#id2958336)

[The Roguelike Pattern](ch11s06.html#id2958491)

[The 'Separated Engine and Interface' Pattern](ch11s06.html#id2958899)

[The CLI Server Pattern](ch11s06.html#id2959821)

[Language-Based Interface Patterns](ch11s06.html#id2959928)

[Applying Unix Interface-Design Patterns](ch11s07.html)

[The Polyvalent-Program Pattern](ch11s07.html#id2960228)

[The Web Browser as a Universal Front End](ch11s08.html)

[Silence Is Golden](ch11s09.html)

12\. [Optimization](optimizationchapter.html)

[Don\'t Just Do Something, Stand There!](ch12s01.html)

[Measure before Optimizing](ch12s02.html)

[Nonlocality Considered Harmful](ch12s03.html)

[Throughput vs. Latency](ch12s04.html)

[Batching Operations](ch12s04.html#id2961306)

[Overlapping Operations](ch12s04.html#id2961372)

[Caching Operation Results](ch12s04.html#binary_caches)

13\. [Complexity](complexitychapter.html)

[Speaking of Complexity](ch13s01.html)

[The Three Sources of Complexity](ch13s01.html#id2964646)

[Tradeoffs between Interface and Implementation Complexity](ch13s01.html#id2964843)

[Essential, Optional, and Accidental Complexity](ch13s01.html#id2961759)

[Mapping Complexity](ch13s01.html#id2961870)

[When Simplicity Is Not Enough](ch13s01.html#id2963237)

[A Tale of Five Editors](ch13s02.html)

[ed](ch13s02.html#id2963445)

[vi](ch13s02.html#vi_complexity)

[Sam](ch13s02.html#id2963798)

[Emacs](ch13s02.html#emacs_editing)

[Wily](ch13s02.html#id2967110)

[The Right Size for an Editor](ch13s03.html)

[Identifying the Complexity Problems](ch13s03.html#id2967267)

[Compromise Doesn\'t Work](ch13s03.html#id2967642)

[Is Emacs an Argument against the Unix Tradition?](ch13s03.html#id2967765)

[The Right Size of Software](ch13s04.html)
:::
::::::

::: navfooter

------------------------------------------------------------------------

  -------------------------------------- ----------------------------------- ------------------------------------------------
  [Prev](ch03s03.html){accesskey="p"}      [Up](index.html){accesskey="u"}      [Next](modularitychapter.html){accesskey="n"}
  What Goes Around, Comes Around          [Home](index.html){accesskey="h"}                             Chapter 4. Modularity
  -------------------------------------- ----------------------------------- ------------------------------------------------
:::
