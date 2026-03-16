# SCO\'s Evidence: This Smoking Gun Fizzles Out

Version 1.0 \-- first general release 20 August 2003.

Version 1.1 \-- note significance of the [missing 32V copyright](smoking-fizzle.html#no_c).

Version 1.2 \-- corrected description of the locking calls, added SIII.

*Executive summary: There are three pieces of good news for SCO about the evidence they revealed on 18 August 2003. One is that the evidence does support a claim of code-copying; the second is that GPL is not in this case a usable defense; and the third is that BSD probably doesn\'t save us either. But the rest of the news is all bad for SCO: most of the supposedly infringing code was (a) released as open source by SCO/Caldera in 2002, (b) didn\'t come through IBM or Sequent, (c) isn\'t present in 90% of all running Linux distributions, and (d) was removed from Linux 2.5 in July 2003 on grounds of being too ugly to live. If this is representative of the quality of SCO\'s evidence, their case is dead on arrival.*

## Introduction

At SCOforum on 18 August 2003, SCO displayed a piece of what it called evidence that it owns huge portions of the Linux source code. This is one of the central contention in its [billion-dollar lawsuit against IBM](http://www.opensource.org/sco-vs-ibm.html). The \'evidence\' was two presentation slides showing, side by side, code SCO labeled \"System V\" and "Linux". The first is captioned "Line by line Copying --- One Example of Many "

It\'s now barely 24 hours since the slides leaked. There have been a couple of early analyses published already on [Slashdot](http://slashdot.org/articles/03/08/19/1523236.shtml?tid=106&tid=185) and [Linux Weekly News](http://lwn.net/Articles/45019/). I\'ve written this one because (a) none of these were aimed at a general or journalistic audience, and (b) they miss or don\'t highlight some interesting details that bear on SCO\'s case against IBM and the legality of its licensing program. Also, I\'m doing what others have not dared: I\'m publishing the differences with the relevant System V code.

## The evidence

Let\'s begin by looking at the actual evidence. The original slides are [here](http://www.heise.de/newsticker/data/jk-19.08.03-000/imh0.jpg) and [here](http://www.heise.de/newsticker/data/jk-19.08.03-000/imh1.jpg). SCO\'s display was incomplete, and part of the \"System V\" comment was obfuscated by being transliterated into Greek letters. After undoing the obfuscation, we have the following header comment from what SCO labels \"System V\" code:

Slide 1, left side (\"System V code\"):

    /*
     * Allocate 'size' units from the given map.
     * Return the base of the allocated space.
     * In a map, the addresses are increasing and the
     * list is terminated by a 0 size.
     * The swap map unit is 512 bytes
     * Algorithm is first-fit.
     *
     * As part of the kernel evolution toward modular naming, the functions
     * malloc, and mfree are being renamed to rmalloc and rmfree.
     * Compatibility will be maintained by the following assembly code:
     * (also see mfree/rmfree below)
     */

Slide 1, right side (\"Linux Kernel Code\"):

    /*
     * Allocate 'size' units from the given map.
     * Return the base of the allocated space.
     * In a map, the addresses are increasing and the
     * list is terminated by a 0 size.
     * Algorithm is first-fit.
     */

    ulong_t
    atealloc(
        struct map *mp,
        size_t size)
    {
        register unsigned int a;
        register struct map *bp;
        register unsigned long s;

Slide 2 simply shows a portion of the Linux kernel code:

        if (size == 0)
            return((ulong_t) NULL);

        s = mutex_spinlock(maplock(mp));

        for (bp = mapstart(mp); bp->m_size; bp++) {
            if (bp->m_size >= size) {
                a = bp->m_addr;
                bp->m_addr += size;
                if ((bp->m_size -= size) == 0) {
                    do {
                        bp++;
                        (bp-1)->m_addr = bp->m_addr;
                    } while ((((bp-1)->m_size) = (bp->m_size)));
                    mapsize(mp)++;
                }

                ASSERT(bp->m_size < 0x80000000);
                mutex_spinunlock(maplock(mp), s);

Observe that SCO does not actually show the System V code, but only the comment.

On the Linux side, this code is in the 2.4 file [arch/ia64/sn/io/ate_utils.c](http://ftp.kernel.org/pub/linux/kernel/people/marcelo/linux-2.4/arch/ia64/sn/io/ate_utils.c). Here is the entire text of the relevant function:

    /*
     * Allocate 'size' units from the given map.
     * Return the base of the allocated space.
     * In a map, the addresses are increasing and the
     * list is terminated by a 0 size.
     * Algorithm is first-fit.
     */

    ulong_t
    atealloc(
        struct map *mp,
        size_t size)
    {
        register unsigned int a;
        register struct map *bp;
        register unsigned long s;

        ASSERT(size >= 0);

        if (size == 0)
            return((ulong_t) NULL);

        s = mutex_spinlock(maplock(mp));

        for (bp = mapstart(mp); bp->m_size; bp++) {
            if (bp->m_size >= size) {
                a = bp->m_addr;
                bp->m_addr += size;
                if ((bp->m_size -= size) == 0) {
                    do {
                        bp++;
                        (bp-1)->m_addr = bp->m_addr;
                    } while ((((bp-1)->m_size) = (bp->m_size)));
                    mapsize(mp)++;
                }

                ASSERT(bp->m_size < 0x80000000);
                mutex_spinunlock(maplock(mp), s);
                return(a);
            }
        }

        /*
         * We did not get what we need .. we cannot sleep .. 
         */
        mutex_spinunlock(maplock(mp), s);
        return(0);
    }

The code in question is a memory-allocation routine intended to be used by other code in the kernel. We can\'t see exactly which code SCO is referring to in its Unixware tree, but there is indeed a very similar implementation in several Unixes.

Almost the earliest version of Unix for which sources are still extant is Fifth Edition (aka Version 5 or V5), released 1974. Here is the [Fifth Edition](http://minnie.tuhs.org/UnixTree/V5/usr/sys/ken/malloc.c.html) version of the code in question. with a copyright date of 1973.

    malloc(mp, size)
    struct map *mp;
    {
        register int a;
        register struct map *bp;

        for (bp = mp; bp->m_size; bp++) {
            if (bp->m_size >= size) {
                a = bp->m_addr;
                bp->m_addr =+ size;
                if ((bp->m_size =- size) == 0)
                    do {
                        bp++;
                        (bp-1)->m_addr = bp->m_addr;
                    } while ((bp-1)->m_size = bp->m_size);
                return(a);
            }
        }
        return(0);
    }

Here is the [Sixth Edition](http://minnie.tuhs.org/UnixTree/V6/usr/sys/ken/malloc.c.html) (or V6) version from 1976. An added comment is highlighted in red; otherwise the code is identical to the V5 version.

    /*
     * Allocate 'size' units from the given
     * map. Return the base of the allocated
     * space.
     * Algorithm is first-fit.
     */
    malloc(mp, size)
    struct map *mp;
    {
        register int a;
        register struct map *bp;

        for (bp = mp; bp->m_size; bp++) {
            if (bp->m_size >= size) {
                a = bp->m_addr;
                bp->m_addr =+ size;
                if ((bp->m_size =- size) == 0)
                    do {
                        bp++;
                        (bp-1)->m_addr = bp->m_addr;
                    } while ((bp-1)->m_size = bp->m_size);
                return(a);
            }
        }
        return(0);
    }

The version 6 code appears in [Lions Commentary on Unix](http://www.amazon.com/exec/obidos/tg/detail/-/1573980137/ref=lib_dp_TFCV/002-5014074-3489645?v=glance&s=books&vi=reader#reader-link), composed in 1975-76. The Lions book (with included source code) was republished with SCO\'s blessing in 1996.

Here is the [Version 7](http://minnie.tuhs.org/UnixTree/V7/usr/sys/sys/malloc.c.html) code from 1979. Again, differences from the previous version (V6) are highlighted in red; the differences are trivial and reflect minor changes in the syntax and type-declaration facilities of C.

    /*
     * Allocate 'size' units from the given
     * map. Return the base of the allocated
     * space.
     * In a map, the addresses are increasing and the
     * list is terminated by a 0 size.
     * The core map unit is 64 bytes; the swap map unit
     * is 512 bytes.
     * Algorithm is first-fit.
     */
    malloc(mp, size)
    struct map *mp;
    {
        register unsigned int a;
        register struct map *bp;

        for (bp=mp; bp->m_size; bp++) {
            if (bp->m_size >= size) {
                a = bp->m_addr;
                bp->m_addr += size;
                if ((bp->m_size -= size) == 0) {
                    do {
                        bp++;
                        (bp-1)->m_addr = bp->m_addr;
                    } while ((bp-1)->m_size = bp->m_size);
                }
                return(a);
            }
        }
        return(0);
    }

Here is the version from [32V](http://minnie.tuhs.org/UnixTree/32VKern/usr/src/sys/sys/malloc.c.html), dating from later in 1979. Again, differences from the previous version (V7) are highlighted in red; the only one is a minor tweak to the header comment.

    /*
     * Allocate 'size' units from the given
     * map. Return the base of the allocated
     * space.
     * In a map, the addresses are increasing and the
     * list is terminated by a 0 size.
     * The swap map unit is 512 bytes.
     * Algorithm is first-fit.
     */
    malloc(mp, size)
    struct map *mp;
    {
        register unsigned int a;
        register struct map *bp;

        for (bp=mp; bp->m_size; bp++) {
            if (bp->m_size >= size) {
                a = bp->m_addr;
                bp->m_addr += size;
                if ((bp->m_size -= size) == 0) {
                    do {
                        bp++;
                        (bp-1)->m_addr = bp->m_addr;
                    } while ((bp-1)->m_size = bp->m_size);
                }
                return(a);
            }
        }
        return(0);
    }

The System III version from 1981 is identical to the 32V version except that there\'s a trivial whitespace change in the comment.

Allowing for comment tweaks and minor language changes, the V5/V6/V7/32V/SIII versions are identical. This is very stable code implementing a simple algorithm. We\'ll call it the "ancient" version and take the 32V/SIII code as representative.

Now, here is the Linux version again. This time, differences from the ancient version are highlighted in red. Trivial differences in whitespace distribution are ignored.

    /*
     * Allocate 'size' units from the given map.
     * Return the base of the allocated space.
     * In a map, the addresses are increasing and the
     * list is terminated by a 0 size.
     * Algorithm is first-fit.
     */

    ulong_t
    atealloc(
        struct map *mp,
        size_t size)
    {
        register unsigned int a;
        register struct map *bp;
        register unsigned long s;

        ASSERT(size >= 0);

        if (size == 0)
            return((ulong_t) NULL);

        s = mutex_spinlock(maplock(mp));

        for (bp = mapstart(mp); bp->m_size; bp++) {
            if (bp->m_size >= size) {
                a = bp->m_addr;
                bp->m_addr += size;
                if ((bp->m_size -= size) == 0) {
                    do {
                        bp++;
                        (bp-1)->m_addr = bp->m_addr;
                    } while ((((bp-1)->m_size) = (bp->m_size)));
                    mapsize(mp)++;
                }

                ASSERT(bp->m_size < 0x80000000);
                mutex_spinunlock(maplock(mp), s);
                return(a);
            }
        }

        /*
         * We did not get what we need .. we cannot sleep .. 
         */
        mutex_spinunlock(maplock(mp), s);
        return(0);
    }

These are small differences. Most are trivial. The expression in the while loop differs only in having two extra layers of parentheses. The `size_t` parameter is declared rather than being allowed to default to an int. `mapstart` and `mapsize` are trivial macro. The only significant changes are the addition of the assertions and the lock-map handling.

Another [version of the same code](http://unix-archive.pdp11.org.ru/PDP-11/Trees/2.11BSD/sys/sys/subr_rmap.c) is in the 2.11 BSD Unix system makes a useful contrast. The 2.11 version is much more heavily commented and has elaborations the 32V version lacks; it is genuinely different. Here it is:

    /*
     * Allocate 'size' units from the given map.  Return the base of the
     * allocated space.  In a map, the addresses are increasing and the
     * list is terminated by a 0 size.
     *
     * Algorithm is first-fit.
     */
    memaddr
    malloc(mp, size)
        struct map *mp;
        register size_t size;
    {
        register struct mapent *bp, *ep;
        memaddr addr;
        int retry;

        if (!size)
            panic("malloc: size = 0");
        /*
         * Search for a piece of the resource map which has enough
         * free space to accomodate the request.
         */
        retry = 0;
    again:
        for (bp = mp->m_map; bp->m_size; ++bp)
            if (bp->m_size >= size) {
                /*
                 * Allocate from the map.  If we allocated the entire
                 * piece, move the rest of the map to the left.
                 */
                addr = bp->m_addr;
                bp->m_size -= size;
                if (bp->m_size)
                    bp->m_addr += size;
                else for (ep = bp;; ++ep) {
                    *ep = *++bp;
                    if (!bp->m_size)
                        break;
                }
    #ifdef UCB_METER
                if (mp == coremap)
                    freemem -= size;
    #endif
                return(addr);
            }
        /* no entries big enough */
        if (!retry++) {
            if (mp == swapmap) {
                printf("short of swap\n");
                xumount(NODEV);
                goto again;
            }
            else if (mp == coremap) {
                xuncore(size);
                goto again;
            }
        }
        return((memaddr)NULL);
    }

And now\...tadaaa!\...the System V Release 4 version, in uts/i386/os/malloc.c. As a way of avoiding a technical copyright violation, I\'m not going to give the SVr4 source itself. (I acquired it back in the 1980s when bootleg System V source trees were fairly commonly passed around among System V administrators and developers; vendors knew of this but ignored it as long as the tapes weren\'t used to create unlicensed installations.) Instead of showing the code, I\'m going to show you something that is actually more informative; a diff between the SVr4 version and the Linux version.

Any SCO lawyers tempted to make a fuss over the publication of these diffs or my access to the SVr4 code should think carefully about the sorts of things that happen to corporations with already poor reputations who try to sue journalists engaged in fact publication with respect to a dispute of wide public interest.

In fact, publishing the code itself would arguably have been legal. In his ruling on the 1993 denial of injunction that led to the settlement, the judge [expressed doubt](http://cm.bell-labs.com/cm/cs/who/dmr/bsdi/930303.ruling.txt) that AT&T held any legitimate copyright in the bulk of the Unix code at all (see my [No Secrets](http://www.catb.org/~esr/nosecrets/) page for related discussion). If I were SCO\'s lawyers, the last thing I\'d want is to re-open that can of worms. What stopped me wasn\'t legal risk but the ethical problem; I respect intellectual-property rights and don\'t want to violate SCO\'s even incidentally, even after the blatant disregard they\'ve shown for my rights as an issuer of code under the GPL.

Here is the diff. Lines beginning with \< mark lines not actually present in the Linux version; lines beginning with \> mark lines in the Linux code not in the SVr4 code. The format has been chosen to illustrate the fact that the differences between the SVr4 and Linux versions are mostly trivial syntax-level stuff. But there are real differences: the fact that the System V function is split in two (`rmalloc` and the `malloc` wrapper) and the calls to the lock/unlock functions.

    6d5
    <  * The swap map unit is 512 bytes.
    8,12d6
    <  *
    <  * As part of the kernel evolution toward modular naming, the
    <  * functions malloc and mfree are being renamed to rmalloc and rmfree.
    <  * Compatibility will be maintained by the following assembler code:
    <  * (also see mfree/rmfree below)
    15,26c9,12
    < unsigned long
    < malloc(mp, size)
    < register struct map *mp;
    < register size_t size;
    < {
    <       return(rmalloc(mp, size));
    < }
    <
    < unsigned long
    < rmalloc(mp, size)
    < register struct map *mp;
    < register size_t size;
    ---
    > ulong_t
    > atealloc(
    >       struct map *mp,
    >       size_t size)
    30c16,18
    <       register int s;
    ---
    >       register unsigned long s;
    >
    >       ASSERT(size >= 0);
    33,35c21,24
    <               return(NULL);
    <       ASSERT(size > 0);
    <       s = splhi();
    ---
    >               return((ulong_t) NULL);
    >
    >       s = mutex_spinlock(maplock(mp));
    >
    44c33
    <                               } while ((bp-1)->m_size = bp->m_size);
    ---
    >                               } while ((((bp-1)->m_size) = (bp->m_size)));
    47,48c36,38
    <                       ASSERT(bp->m_size < (unsigned)0x80000000);
    <                       splx(s);
    ---
    >
    >                       ASSERT(bp->m_size < 0x80000000);
    >                       mutex_spinunlock(maplock(mp), s);
    52c42,46
    <       splx(s);
    ---
    >
    >       /*
    >        * We did not get what we need .. we cannot sleep ..
    >        */
    >       mutex_spinunlock(maplock(mp), s);

Knowing what I do about the functional changes in UnixWare since SVr4, I would bet the price of a good steak dinner that the UnixWare version of this code is effectively identical to the SVr4 version.

## The similarities

All these pieces of code are sufficiently similar to convince me (or any other competent C programmer) the Linux, 2.11BSD and System V Release 4 versions all derive from the ancient version. The System V and Linux versions really differ from the common ancestor only in that they both contain something that looks like mutual-exclusion locking.

Actually the SVr4 calls aren\'t strictly locking calls but just interrupt disablers; the difference has to do with the fact that SVr4 was not SMP-capable. The SVr4 calls are there to block interrupts (a way of ensuring that the inner code of the function cannot be interrupted by disk events or timer ticks), the Linux ones are there to enable symmetric multiprocessing without corrupting the memory pool. The difference is significant.

The ancient, System V and Linux versions are more alike than any of them resembles the BSD code. The differences among them are exactly the sorts that would be introduced by evolutionary drift as copied code was adapted over time.

In retrospect, there was a clue in the Linux code all along that it had been copied from rather old sources rather than being written fresh: the `register` declarations. Those do by hand an optimization that modern C compilers do automatically, and most programmers lost the habit of inserting them in new code a good ten years ago. So the honest question is: where was Linux\'s `atemalloc` copied from?

To clarify matters, here is a rough similarity tree of the versions of this code. Each arrow is a probable copied-to relationship. Relative distances indicate code similarity; the main point is that the SVr4 code and Linux code are relatively close together, about equally dissimilar from 32V, with 2.11BSD more different.

                                          +------> SVr4
                                          |
                       ancient Unix ----+-|
                                        | |
                                        | +------> Linux
                                        |
                                        | 
                                        +------> 2.11BSD

(Sorry for the ASCII graphics, but I wanted this document to be self-contained HTML.)

One thing that backs up this this reconstruction of the evolutionary tree is that these relationships match the chronology of the releases, as described for example in [Éric Lévénez\'s history chart](http://www.levenez.com/unix/)

So, in alleging copying from old Unix code, SCO is actually on pretty firm ground here. What does this suggest about IP rights or violations in this situation? It depends in which version the code was copied from.

## Who copied from whom?

Based on the similarity tree, the source from which the Linux code was copied is least likely to have been BSD.

In 1993 AT&T\'s Unix Systems Labs (USL) sued BSDI, a company selling the BSD system, and the University of California, over allegedly misappropriated code in the BSD system. Their complaint was quite similar to SCO\'s. They were effectively forced to settle after a judge found that AT&T had flagrantly misappropriated BSD code into its kernel. In the settlement, the University agreed to add an AT&T copyright notice to some files but gained the right to continue to distribute all under the BSD license. AT&T agreed to pay the University\'s court costs. Some details of the lawsuit are [here](http://cm.bell-labs.com/cm/cs/who/dmr/bsdi/bsdisuit.htm).

Some analysts have held that existence of the open-source BSD version is a sufficient shield against charges that the Linux version was stolen from SCO. While I expect that will turn out to be the case for many of the other alleged code overlaps (and indeed I was the [first to suggest this possibility](http://www.opensource.org/sco-vs-ibm.html) back in March 2003), I cannot honestly say that I think it is an applicable defense here. The real question is whether the Linux implementation was originally copied from ancient Unix or System V before being modified to fit the Linux environment.

Before trying to determine this, we need to consider the difference between casual and guilty copying. Casual copying is the cut-and-paste that happens when you\'re sure you have permission to re-use, or aren\'t thinking about it. Guilty copying is when you know you shouldn\'t. Guilty copiers will try to cover their tracks. The easiest way to do this is by changing local variable names, because that sort of change is easy to do without breaking code.

The reason we need to make this distinction is that three of the versions resemble each other so much that if the copier were trying to cover his tracks we couldn\'t rely on any textual clues at all.

Thankfully, we are almost certainly dealing with the results of casual copying here. All the versions use `bp` as the principal local variable. None of the differences between the SVr4 and Linux, or the ancient and Linux versions. look like they were put in to obfuscate similarities. So we\'ll assume that we can actually trust the textual clues.

Given this, there are two pieces of internal evidence that suggest the ancient code. One is that the function is split in two in SVr4 but single in ancient Unix and Linux. A subtler indication is that one change between SVr4 and Linux would remove a cast (in the second `ASSERT` call). It is quite unlikely that a programmer casually copying code would go to the effort to remove a cast, and a guilty copier wouldn\'t do it when there are ways to obscure similarities that are both easier and less likely to spawn subtle bugs. This is especially true since a more effective obscuring method would have been to remove the `ASSERT`s entirely; they are used for debugging rather than being necessary to operation and could be readily dispensed with.

On the other side, the fact that both the SVr4 and Linux versions contain `ASSERT` macros and what look like lock-manipulation calls, while ancient Unix does not, might seem to argue strongly that the Linux code was copied from SVr4. But there is less here than meets the eye. The first `ASSERT` actually *differs* in a way that isn\'t trivial (the Linux version excludes a size argument of zero). And we\'ve already seen that the locking calls are doing significantly different things.

Caldera\'s original complaint asserted that Linux SMP was copied from SVr4, but their revised complaint dropped this claim. It is well documented that Linux SMP was a from-scratch implementation, built by Alan Cox in 1996 using Caldera-supplied equipment. In effect, the locking calls drop out of the diff with ancient Unix; they aren\'t a good fingerprint for copying, because they\'re functionally forced by two different sets of requirements that didn\'t exist in 32V.

Actually, the most convincing case for the Linux code having been copied from SVr4 rests on the `mapstart` and `mapsize` macros. These occur in the Linux and SVr4 versions but not in the ancient code. They are not forced by the requirement to support SMP. The key to understanding these lies in the fact that their implementations in Linux and SVr4 are different --- they\'re access macros for different data structures. They *couldn\'t* have been copied from SVr4 and still worked, because the offsets would have been wrong; rather, it appears that somebody working on the Linux ia64 port tree who had seen SVr4 code before must have implemented these macros locally in order to have familiar interfaces handy. This would be neither surprising nor actionable.

Overall, the evidence we have suggests that the Linux code was copied casually from ancient Unix, rather than maliciously from System V. The malicious-copying theory that SCO\'s case depends on would in this case fail not only the criminal beyond-a-reasonable-doubt test but the civil preponderance-of-the-evidence test.

## Intellectual-property implications

Unfortunately for SCO, the concession that Linux\'s `atemalloc` was probably copied from 32V helps their case not at all. Because the relevant ancient-Unix file, the 32V version, is legally available from [here](http://minnie.tuhs.org/UnixTree/32VKern/usr/src/sys/sys/malloc.c.html).

And why is this code available on the net? Because SCO/Caldera let the 5th Edition, 6th Edition, Version 7, 32V, and System III code go out under a BSD-like license in January of 2002, well before the 2.4.19 patch introduced this code into Linux.

[Here](http://www.lemis.com/grog/UNIX/) is a copy of the letter in which Caldera officially announced the release of the \"ancient Unix\" source trees. Dion Johnson, who signed the letter, described himself as \"Product Manager and one of many open source enthusiasts in Caldera Intl.\" Mr. Johnson\'s letter includes a pointer to the authorizing [license letter](http://www.lemis.com/grog/UNIX/ancient-source-all.pdf). The authorizing letter fails to mention System III, but a copy of the SCO page from which it was offered along with the other ancient Unixes still exists on the [Wayback Machine](http://www.archive.org).

More generally, SCO\'s case is, to say the least, somewhat impaired by the fact that SCO itself freely released all of the code of ancestral Unix. Under the conditions defined by the Ancient Unix license, issued by SCO/Caldera itself, the Linux kernel developers could copy the entire ancient Unix source tree into the kernel and SCO/Caldera would have no proprietary claim on the results whatsoever.

The fact that closely descendant code appears in System V helps them not at all. To make their case, they\'d have to show that substantial code which was *not present in any open-source Unix kernel* was copied into the Linux kernel. This will, at minimum, be difficult.

## Provenance and other details

But we\'re not done. There are at least three more interesting details about this code. Here they are:

1.  The Linux code is in the ia64 port, not the i386 port as in SVr4.
2.  It came from SGI, not IBM or Sequent.
3.  It was introduced in 2.4.19 and removed in 2.5.
4.  The 32V code has no copyright.

Each of these has some significance for SCO\'s case. I\'ll explain.

This code occurs in the ia64 port for the Itanium processor, not in the main port tree for 32-bit Intel processors. This means that upwards of 90% of all Linux users, including the corporate users SCO is now shaking down for license fees, are running binary Linux distributions that *do not include this code*. That\'s right, SCO is threatening them over code that isn\'t compiled into their kernels and is probably not present as source anywhere on their production systems!

The copyright on the Linux file is by Silicon Graphics, Inc --- which is consistent with what\'s in many other sources files. Much of the NUMA work SCO claims was its own was also contributed by SGI. None of this much helps SCO\'s contract-violation case, which is based on a claim that System V code was wilfully misappropriated by IBM and Sequent in a conscious attempt to destroy SCO\'s Unix business.

The timing of the code\'s introduction and removal is significant in two ways, one negative and one positive. Negative first: this `atemalloc` code was introduced in 2.4.19. Thus, GPL would *not be a defense against SCO\'s charges* in this case, because the last kernel SCO distributed was 2.4.13.

Now positive: the code was removed from 2.5 in July 2003, not because of copyright issues but because it was an ugly kluge. So in the current version of Linux, this code is not even present in the ia64 port!

The [thread](http://marc.theaimsgroup.com/?l=linux-kernel&m=105618426518781&w=2) surrounding the removal is interesting. In it, for example, Manfred Spraul of the kernel list wrote:

> P.S.: I\'d propose that the GPL rule that a change must be tagged with the name of the person who changes (or adds) a file is enforced - atealloc.c is only tagged with \"SGI\", thus I don\'t know who should be shot for writing that.

It\'s difficult to imagine anything less indicative of a conspiracy (by IBM or anyone else) to mulct SCO of their intellectual property or obscure the trail of kernel changes. First, Spraul is advocating that the origin of changes to the kernel code should be tracked *more closely* so their owners can be discovered. Second, he is doing so because in this case the result of importing the code was crap.

[]{#no_c}

## The Curious Case of the Missing Copyright

The 1979 [32V code](http://minnie.tuhs.org/UnixTree/32VKern/usr/src/sys/sys/malloc.c.html) has no explicit copyright in it. This matters, because under U.S. copyright law before 1996, AT&T failed the limited-publication test for retaining implicit copyright in a published work. This is why the judge in the AT&T-vs.BSD lawsuit issued a [ruling](http://cm.bell-labs.com/cm/cs/who/dmr/bsdi/930303.ruling.txt) doubting that AT&T could sustain its copyright claim, which in turn is why AT&T settled. They knew that if it came to a stand-up fight in a courtroom, they would probably lose *all* rights in the code.

The law was changed in 1996 in ways that made implicit copyrights much stronger and easier to defend. (No, this wasn\'t a nefarious plot by the RIAA, it was to bring U.S. Law in line with the international Berne Convention on copyrights.)

SCO, as AT&T\'s successor in interest, is thus heir to a serious problem. There have been so many copies of the ancient Unix sources floating around for so long that it\'s genuinely unclear whether they have copyright control over them. Those of you like me with sources of System V that we acquired before 1996 can\'t be sued for possession, both because of the pre-1996 rules and because the three-year limitation on copyright prosecutions is long exceeded. (We could still be sued for republishing them; that would be a new violation.)

And, in fact, with respect to any code copying that might have been done more than three years ago, SCO has no ability to recover damages for copyright violation whether the sources leaked out before or after 1996.

## Conclusion

So, in summary, SCO is right where it doesn\'t matter and wrong where it does. Yes, it does appear that in this case code was copied into Linux from older Unix versions. But because the relevant ancestral code was released in open source by SCO/Caldera before it was incorporated, SCO/Caldera has no case here.

You might wish to read [Greg Lehey\'s analysis](http://www.lemis.com/grog/SCO/code-comparison.html) of this code. He differs on some points but reaches the same overall conclusion.

There was also an analysis by [Bruce Perens](http://www.perens.com/SCO/SCOCopiedCode.html) that developed to include a couple more slides.
