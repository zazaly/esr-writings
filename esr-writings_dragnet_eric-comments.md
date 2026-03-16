::: {#Header}
  ---------------------------------- --
  Epilogue: The Making of DRAG.NET   
  ---------------------------------- --
:::

::: {#Menu}

------------------------------------------------------------------------

[Home Page](http://www.catb.org/~esr "My home page")\
[What\'s New](http://www.catb.org/~esr/whatsnew.html "What"){s="" new="" on="" this="" site'\"=""}\
[Site Map](http://www.catb.org/~esr/sitemap.html "Map of the site")\
[Software](http://www.catb.org/~esr/software.html "Software I maintain")\
[Projects](http://www.catb.org/~esr/projects.html "My projects")\
[HOWTOs](http://www.catb.org/~esr/faqs/ "My FAQ documents")\
[Essays](../index.html "Essays and ruminations")\
[Personal](http://www.catb.org/~esr/personal.html "Portrait of the author")\
[Weblog](http://armedndangerous.blogspot.com)\
[Freedom!](http://www.catb.org/~esr/netfreedom/)\
[Firearms!](http://www.catb.org/~esr/guns/)\

------------------------------------------------------------------------
:::

::: {#Content}
Since making presentations like this one is a significant application area for many non-technical users, there are some useful lessons in our experience putting this production together.

No proprietary software was used in the making of this production. No animals were harmed, either, although we did brainstorm it over a couple of damn good steak dinners.

We used [xsane 0.77](http://www.xsane.org/) with an Epson Perfection 1650 scanner for photograph capture. This combination worked extremely well. Kudos to the authors of xsane for excellent work; the only two nits we found were that it really ought to default to color mode, and needs to handle out-of-memory errors induced by very large image dumps more gracefully.

We heartily recommend the [Perfection 1650](http://www.epson.com/cgi-bin/Store/ProductQuickSpec.jsp?BV_SessionID=@@@@0701153446.1012160183@@@@&BV_EngineID=eadcddlmdlmibfdmcfjgckidnf.0&oid=6464130&category=Products) to anyone looking for a quality scanner at a good price. Epson has cooperated well with the open-source community, and the results do all parties proud.

Before we settled on the Epson, we had a very\...educational\...experience with a \$40 scanner that shall remain nameless. It claimed to be a USB scanner, but lied \-- it required a proprietary firmware upload at initialization time and would not work with Linux\'s USB scanner driver. Yes, we encountered a WinScanner! Stay out of the price basement; it\'s more trouble than it\'s worth.

We did image conversion, cropping and resizing using the ImageMagick convert(1) and display(1) tools. The xwd(1) utility was used to capture screen displays. All these programs worked well and without fuss.

The presentation was sequenced with Kpresenter (from koffice 1.1), which is marginally usable but in no way ready for the non-techie. The UI is cluttered, inconsistent, confusing, and at times capricious. We tripped over many bugs and instabilities, and hung it at least a dozen times during simple, basic operations like resizing text. It is also very poorly documented, and uses an opaque binary file format.

(I have since been told that the \"opaque binary file format\" is actually a tar archive of XML files and PNG images. That\'s still opaque, since as far as I know this fact is not documented, and it\'s still binary.)

Kpresenter\'s most serious flaw was functional \-- no way to associate sound clips with the slides. As a result, we experimented with using a browser in full-screen mode as a presentation engine, only to discover that embedding sound in in local web pages is unusably flaky. We couldn\'t get it to work in either Mozilla or Konqueror, and for the same reason. Both paint the web page twice, and spawn two sound helpers that fight with each other.

As a result, we ended up planning to drive the presentation visuals and sound from two different computers, with manual sequencing. This *must* be fixed if kpresenter is going to be competitive \-- because the night before going to LWE, I found MagicPoint.

MagicPoint is a rather more powerful and simpler presentation package than kpresenter. It can attach sound clips to slides and do all manner of other interesting things that kpresenter cannot, including allowing you to scribble on a slide while it is being displayed.

MagicPoint has only one drawback: no GUI. You write your slides in a simple markup language, bashing tags with a text editor. This is great for geeks but a deadly turnoff to end-users. Someone could do the world a great service by writing a GUI editor for MagicPoint files.

About those sound clips\...we found a clean MP3 of the entire Dragnet theme on the Web. When it became apparent that we would need to drop out the middle section with the voiceover, I went looking for an MP3 audio editor. We found one: [Audacity](http://audacity.sourceforge.net/). I love this piece of software \-- it\'s beautifully designed, has a clean and readily accessible UI, and is excellently documented to boot. Using it helped banish the bad taste kpresenter had left in our mouths.

We tripped over a couple of dozen embarrassing bugs in a few days\' work. We have no doubt that all could easily be fixed. Our experience suggests that the problem with open-source applications is not poor design or implementation, it\'s inadequate testing. The usage patterns of developers don\'t match those of end-users, so they sail right by the bugs that actual users would trip right over and be immediately turned off by.

It\'s a self-reinforcing problem \-- untested software drives away real users, so it never gets properly tested, so it never gets good enough not to drive away users. Somehow we need to set up more tests with ordinary users.

The software we had to learn to use during production refutes the canard that Linux hackers as a group are hopelessly bad at interface design for non-techies. Rather, open source completely spans the gamut \-- from clumsy, overcomplex and brittle UIs like that of kpresenter, through excellent if somwhat complex interfaces like that of xsane, all the way to superbly simple UIs like that of audacity.

Audacity has a UI as good or better than the average Macintosh application. That\'s where we need to be for Linux on the desktop to stop being a subject for vaudeville routines, and start being an unstoppable tide.
:::
