::: NAVHEADER
  The Ultimate Linux Box 2001: How to Design Your Dream Machine: (Bigger, Longer, and Uncut)      
  -------------------------------------------------------------------------------------------- -- ------------------------------------------------
  [\<\<\< Previous](ulb2001.html){accesskey="P"}                                                    [Next \>\>\>](economizing.html){accesskey="N"}

------------------------------------------------------------------------
:::

::: SECT1
What To Optimize

Most people think of the processor as the most important choice in specifying any kind of personal-computer system. But for typical job loads under Linux, the processor type is nearly a red herring --- it\'s far more important to specify a capable system bus and disk I/O subsystem. If you don\'t believe this, you may find it enlightening to keep [[top]{.REFENTRYTITLE}(1)]{.CITEREFENTRY} running for a while as you use your machine. Notice how seldom the CPU idle percentage drops below 90%!

It\'s true that after people upgrade their motherboards they often do report a throughput increase. But this is often more due to other changes that go with the processor upgrade, such as improved cache memory or an increase in the clocking speed of the system\'s front-side bus (enabling data to get in and out of the processor faster).

If you\'re buying for Linux on a fixed budget, it makes sense to trade away some excess processor clocks to get a faster bus and disk subsystem. If you\'re building a ULB, go ahead and buy that fastest available processor \-- but once you\'ve gotten past that gearhead desire for big numbers, pay careful attention to bus speeds and your disk subsystem, because that\'s where you\'ll get the serious performance wins. The gap between processor speed and I/O subsystem throughput has only widened in the last five years, so this is even better advice than it was in 1996.

How does it translate into a recipe in 2001? Like this:

-   *Do* get a pure PCI-bus machine (not a hybrid PCI/ISA design, you sacrifice about 10% of peak performance with those).

-   *Do* buy a machine with the fastest available \"front-side\" (e.g. processor-to-memory) bus. (In August 2001 the maximum is 266 MHz.)

-   *Do* get a high-speed SCSI controller and the fastest SCSI disks you can get your hands on.

The case for SCSI is a little less obvious but still compelling. For starters, SCSI is still at least 10%-15% faster than IDE/ATAPI running flat out. Furthermore, IDE/ATAPI is still something of a bad kludge. Like Windows, it\'s layered over an ancestral design (ST-506) that\'s antiquated and prone to failure under stress. SCSI, on the other hand, was designed from the beginning to scale up well to high-speed, high-throughput systems. Because it\'s perceived as a \"professional\" choice, SCSI peripherals are generally better engineered than IDE/ATAPI equivalents, and new high-performing drive technologies tend to become available in SCSI first. You\'ll pay a few dollars more, but for Linux the cost is well repaid in increased throughput and reliability.

Rick comments: \"They call me a SCSI bigot. So be it \-- but my hardware keeps being future-proof, I don\'t have to run bizarre emulation layers to address CDRs, I never run low on IRQs or resort to IRQ-sharing (on account of 3-4 ATA controllers each needing one, plus special adapters for scanners, etc.), all my hard drives have hardware-level hot-fix, all my hard disk/CD/tape/etc. devices support a stable standard rather than this month\'s cheap extension kludge, and I don\'t have to worry about adverse interactions at the hardware or driver levels from mixing ATA and SCSI.\" He speaks for all three of us. Neither Daryll nor I will have IDE in any machine we build either, though we grudgingly tolerate it in our laptops.

For the fastest disks you can find, pay close attention to average seek and latency time. The former is an average time required to seek to any track; the latter is the maximum time required for any sector on a track to come under the heads, and is a function of the disk\'s rotation speed.

Of these, average seek time is *much* more important. When you\'re running Linux or any other virtual-memory operating system, a one millisecond faster seek time can make a really substantial difference in system throughput. Back when PC processors were slow enough for the comparison to be possible (and I was running System V Unix), it was easily worth as much as a 30MHz increment in processor speed. Today the corresponding figure would probably be as much as 300MHz!

The manufacturers themselves avoid running up seek time on the larger-capacity drives by stacking platters vertically rather than increasing the platter size. Thus, seek time (which is proportional to the platter radius and head-motion speed) tends to be constant across different capacities in the same product line. This is good because it means you don\'t have to worry about a capacity-vs.-speed tradeoff.

The cutting edge in SCSI devices is ultra wide LVD (low-voltage-differential) SCSI drives with 160MB/sec transfer speed, running over a 68-pin cable. Vendors often call this combination \"SCSI-3\", which is incorrect as most of these devices don\'t have built-in support for the entire SCSI-3 protocol, and it would be overdesign if they did (the extra commands are designed for use with CD and multimedia devices).

Fast ultra LVD is a bit more expensive to support than the older versions of SCSI (for which key words are \"single-ended\", describing the electrical interface, and \"narrow\", describing the width of data transfers over the older-style 50-pin connector). Thus, you\'re likely to find it only on hard drives that are physically capable of doing high-speed data access off their media; slower devices such as tapes and CD drives are normally still built with the narrow single-ended variant.
:::

::: NAVFOOTER

------------------------------------------------------------------------

  --------------------------------------------------------------- ------------------------------------- ------------------------------------------------
  [\<\<\< Previous](ulb2001.html){accesskey="P"}                   [Home](ulb2001.html){accesskey="H"}    [Next \>\>\>](economizing.html){accesskey="N"}
  The Ultimate Linux Box 2001: How to Design Your Dream Machine                                                            But What If I\'m Economizing?
  --------------------------------------------------------------- ------------------------------------- ------------------------------------------------
:::
