::: NAVHEADER
  The Ultimate Linux Box 2001: How to Design Your Dream Machine: (Bigger, Longer, and Uncut)      
  -------------------------------------------------------------------------------------------- -- -----------------------------------------------
  [\<\<\< Previous](configuration.html){accesskey="P"}                                              [Next \>\>\>](references.html){accesskey="N"}

------------------------------------------------------------------------
:::

::: SECT1
Conclusion

I find it impressive that, after having specified it on a cost-is-no-object basis, the the total system cost is nevertheless so low. I tried hard to gold-plate as much of the system as possible and load on all the extras and accessories I could, and was nevertheless unable to raise the total parts bill over \$7000.

It is also interesting that so little of the cost is in the system core. The motherboard, memory, case, cooler and drives are only a hair over \$3200 of the total. If we discarded the most extravagant peripherals \-- dumping the Klipsch speakers and the Radeon and the DVD and DDS drives, the cost would drop to a quite reasonable \$4200 or so. Rick Moen observes pungently that \"People pay more than that for crap computers every day.\"

You could build the ULB yourself from scratch. But, unless you\'re either a very experienced hardware hacker or seriously enough interested in having a learning experience to accept possibly trashing some expensive parts, maybe you shouldn\'t (I wouldn\'t). There are subtle gotchas that can cost you a lot of grief. A good example, Gary tells me, is installing PC coolers \-- if you\'re inexperienced, it\'s pretty easy to use too much pressure and damage the CPU socket, or even to crack the CPU itself.

This design will be available for purchase from Los Alamos Computers as the ULB-200108 (that is, the August 2001 edition of the Ultimate Linux Box). If you buy it from them rather than assembling it yourself, you\'ll save yourself a lot of time and get a machine that has been assembled by a pro, unit-tested and is warranted. You\'ll also, of course, get the latest Linux pre-installed and pre-customized for the hardware.

One mechanical gotcha with this design is that a machine with Silverados in it can\'t be sent through the mail. There is a silver disc (actual silver, the most heat-conductive metal there is) at the bottom of the heat sink which will be damaged by vibrations during shipping if the Silverado is installed. So you\'ll have to do the final assembly of this bit yourself even if you buy from LAC. Fortunately the vendor provides detailed instructions.

And how fast does it build kernels? After \`make clean\', the Ultimate Linux Box builds the ULB\'s 2.4.9 Linux kernel from a cold standing start (**make -j \'MAKE=make -j\' dep; make -j \'MAKE=make -j\' bzImage**) in less than 1 minute and 50 seconds flat. Sweeeet.
:::

::: NAVFOOTER

------------------------------------------------------------------------

  ------------------------------------------------------ ------------------------------------- -----------------------------------------------
  [\<\<\< Previous](configuration.html){accesskey="P"}    [Home](ulb2001.html){accesskey="H"}    [Next \>\>\>](references.html){accesskey="N"}
  Linux Configuration                                                                                          Acknowledgements and References
  ------------------------------------------------------ ------------------------------------- -----------------------------------------------
:::
