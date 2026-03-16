Back to [Eric\'s Home Page](http://www.catb.org/~esr)

Up to [Site Map](http://www.catb.org/~esr/sitemap.html)

\$Date: 2002/07/09 12:17:11 \$

------------------------------------------------------------------------

# Ultimate Linux Box update page {#ultimate-linux-box-update-page align="CENTER"}

It is February 2002 as I write. In the months since the [Ultimate Linux Box](ulb2001.html) article I have collected a few observations and revisions. Later this year I\'ll probably do a full revision; in the mean time, here are the salient points:

## The system core has performed extremely well

The choice of the S2462 motherboard and UltraStar drives drives appears to have been quite sound. The machine is extremely fast and responsive. It has so much raw processor power and I/O bandwidth that response is unimpaired even during heavy operations such as kernel compiles.

## The SB Live! has been a continuing locus of problems

The sound card gave us a lot of grief during the qualification tests. It gave me grief afterwards, too. In December I tried to install a radio card. While rebuilding the kernel to support it, I somehow lost the ability to play CDs to my speakers \-- and was never able to regain it, despite restoring my original configuration and despite a lot of high-powered technical help (including advice from the driver maintainer).

The Linux support for the SB Live! seems to be fragile and flaky. Troubleshooting it turned into a significant time sink and frustration source. In late January I finally got fed up and replaced it with a no-name PCI sound card. Later, the SB Live! went back in, but I\'m now nervous about even upgrading my OS for fear the sound configuration will break again.

## The Antec enclosure was a good call, but\...

The roominess and good design of the Antec 1200 case has helped keep the hassles involved in swapping sound cards, etc. to a minimum. But I might not use it in the next iteration, because\...

## \...the machine is too noisy

The noise-control engineering in the design initially seemed like a success, but normal wear on the fan and disk bearings seems to have partially undone all that effort. After six months of wear the machine is getting loud.

I\'ve gone back and forth on whether we could address this problem by redesigning the cooling system, perhaps going to something like water-cooling or Peltiers. Water-cooling is likely to require a case designed around it.

Examining the results of varying the decibel output of each part suggested that the only way to cut noise significantly is to quiet the noisiest part \-- theoretically the disk drives. But empirical investigation (putting my ear to the parts) suggests that my dB figures are wrong and the case fans are in fact the problem.

So now I\'m looking into ways to (a) decouple the drives from the case via elastomeric shock mounting, (b) prevent case resonance with acoustic foam, and (c) water-cool to get rid of the case-fan noise (water pumps can be *very* quiet).

We could add a big hard drive cooler to the disk drives to damp some vibrations, thus cutting the noise.

## Towards the ULB 2002

The ULB has already been upgraded to 1800 K7s from the original 1200s. This is the 2468 refresh of the 2462 motherboard, now in full production. Unlike its predecessor it can take 4GB rather than just 2GB of memory. Its only near competition seems to be the highest-end Asus motherboards.

Recent results from StorageReview.com suggest that the Seagate Cheetah X15-36LP (36.7 GB Ultra160/m SCSI) and Fujitsu MAM3367 (36 GB Ultra160/m SCSI) have overtaken the IBM UltraStar in performance. The Cheetah drive is the low-noise winner; it also runs cooler than the UltraStar. But the Fujitsu is slightly faster.

A recent [roundup](http://tech-report.com/reviews/2002q2/ati-nvidia/) tells us that the ATI Radeons and NVidia GeForce cards are still top of the heap. The Radeon 64MB card (which seems to have been retroactively named the 8500 64MB) has since been discontinued. We\'ll probably go with the 128MB refresh of the 8500 for the next version.

The new sound card will probably be a [Turtle Beach Santa Cruz](http://www.turtle-beach.com/site/products/santacruz/indetail.asp). The [Soundblaster Audigy](http://www.soundblaster.com/audigy/) was a contender too, but the Turtle Beach card has better frequency response according to the one site that does audio analysis of these boards. Besides, the experience with the SB Live! was\...mixed.

I\'m looking at [Alpha PAL](http://www.alphanovatech.com/) processor heatsinks. These are designed to be actively cooled by a standard 80mm case fan, which can be very quiet.

We\'ll try [Dynamat](http://www.dynamat.com/) insulation for noise reduction. Note: we should take dBA measurements before and after installation.

## The Parts List

-   
-   2 Athlon K7 MP 1.8GHz
-   
-   1 Tyan K7 Thunder S2468UNG
-   
-   8 Kentron 512MB registered DDR RAM, or Corsair CM73SD512R-2100 512MB PC2100 RAM
-   
-   1 Antec Performance 1200 case
-   2 Alpha PAL8045 Athlon heat sink.
-   2 thermally-controlled 8MM low-noise fans for the PAL.

Some of this stuff can be acquired from [endpcnoise.com](http://www.endpcnoise.com/).

------------------------------------------------------------------------

Back to [Eric\'s Home Page](http://www.catb.org/~esr)

Up to [Site Map](http://www.catb.org/~esr/sitemap.html)

\$Date: 2002/07/09 12:17:11 \$

Eric S. Raymond [\<esr@thyrsus.com\>](mailto:esr@thyrsus.com)
