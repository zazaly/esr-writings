::: NAVHEADER
  The Ultimate Linux Box 2001: How to Design Your Dream Machine: (Bigger, Longer, and Uncut)      
  -------------------------------------------------------------------------------------------- -- -----------------------------------------------
  [\<\<\< Previous](horror_story.html){accesskey="P"}                                               [Next \>\>\>](conclusion.html){accesskey="N"}

------------------------------------------------------------------------
:::

:::::: SECT1
Linux Configuration

Here is a detailed recipe for getting the most out of this hardware. This recipe applies to conditions in August 2001. If you are reading this months afterwards you may be able to skip some steps, and of course the software version numbers you want will be different.

How much swap space to allocate on a machine with 2GB core is a vexing theological question that even the wizards of the Linux kernel mailing list can\'t seem to agree on. The usual rule --- twice your amount of physical memory --- would tie up 4GB, which both seems and is ridiculous unless you\'re doing very heavy-duty database work or scientitic computing with *very* large datasets. On the other hand, the advice to top out at 128MB in the Red Hat manual is obsolete, predating the efforts at VM tuning in the 2.4 series. Early 2.4.x kernels wanted more than 2 × RAM; more recent ones (2.4.8) use less swap.

A better way, according to Arjan de Ven of Red Hat, is to try to estimate the size of your working set (the core utilization of your typical mix of programs) and allocate 150% of that. For people doing typical workstation or light-duty server workloads, the working set is unlikely to go above 128MB. But 2.4.8 and later kernels permit swap partions up to 64GB in size.

::: PROCEDURE
1.  Remove the SB Live!, so your pre-2.4.8 kernel won\'t hang.

2.  Disable the ATA controller and set \"Use PCI Interrupt Entries In MP Table\" in the BIOS configuration screen as you reboot.

3.  Install KRUD or your favorite distribution in text mode. If your X version lacks the Radeon timing patch, be sure to tell your distribution that logins should come up in text mode too, otherwise your first login may get clobbered by the Radeon timing bug.

4.  If your X version lacks the Radeon timing patch, hack your XF86Config-4 to turn off acceleration. This will make it safe to use X until you can patch it.

5.  Download and install a 2.4.8+ kernel (see below).

6.  Power down, re-install your SB Live!, and boot into 2.4.8+. You can now have sound without system hangs.

7.  If your X has the Radeon timing patch, you\'re done. Otherwise\...

8.  Download the X source tree. If it requires the Radeon timing patch (see below) apply that patch. Build it.

9.  Copy the rebuilt X server (`XFree86`{.FILENAME}) to wherever it lives on your system (usually `/usr/X11R6/bin/XFree86`{.FILENAME}) Then copy the Radeon X module `radeon_drv.o`{.FILENAME} to where it lives (usually `/usr/X11R6/lib/modules/drivers/radeon_drv.o`{.FILENAME}).

10. You can now re-enable acceleration and the hardware cursor support.
:::

Here are the things you need to know about your XFree86 configuration file (normally `/etc/X11/XF86Config-4`{.FILENAME}).

::: PROCEDURE
1.  If your installer only autodetects available screen resolutions up to 1600x1200, then you\'ll want to change the Modes entry in the Screen section corresponding to the Radeon device so it reads 2048x1536.

2.  Next, set your mouse protocol to \"MouseManPlusPS/2\", if you didn\'t already during the distribution install; you will get the use of the mouse wheel \-- it will work X scrollbars. Look in the the Input Device section corresponding to your PS/2 mouse.

3.  If you need to temporarily disable acceleration in order not to trigger the Radeon timing bug, look in the Device section corresponding to the Radeon. You\'ll need to insert an option line that reads \"Option NoAccel\".
:::

The change in the third step will be backed out after we fix X.

Here are the kernel configuration options you must specify to get full support for your ULB hardware:

::: TABLE
[]{#AEN604}

**Table 2. ULB kernel configuration symbols (2.4.8)**

  Symbol                                                                                       Value(s)   Description
  -------------------------------------------------------------------------------------------- ---------- -----------------------------------------------------------------------
  General options                                                                                         
  CONFIG_MK7                                                                                   Y or M     Athlon/Duron/K7
  CONFIG_SMP                                                                                   Y          Symmetric Multi-Processing support
  CONFIG_HIGHMEM4G                                                                             Y          High memory support (up to 4G)
  System buses                                                                                            
  CONFIG_PCI                                                                                   Y          Support for PCI bus hardware
  CONFIG_PNP                                                                                   Y or M     Support for Plug\'n\'Play hardware.
  CONFIG_USB                                                                                   Y or M     Universal Serial Bus support
  Graphics options                                                                                        
  CONFIG_AGP                                                                                   Y or M     /dev/agpgart (AGP Support)
  CONFIG_DRM                                                                                   Y          Direct Rendering Manager (XFree86 DRI support)
  CONFIG_DRM_RADEON                                                                            Y          ATI Radeon
  SCSI options                                                                                            
  CONFIG_SCSI                                                                                  Y          SCSI support
  CONFIG_BLK_DEV_SD                                                                            Y          SCSI disk support
  CONFIG_BLK_DEV_ST                                                                            Y or M     SCSI tape support
  CONFIG_BLK_DEV_SR                                                                            Y          SCSI CD-ROM support
  CONFIG_SCSI_AIC7XXX                                                                          Y          Adaptec AIC7xxx support
  Networking options                                                                                      
  CONFIG_NET                                                                                   Y          Networking support
  CONFIG_NET_ETHERNET                                                                          Y          Ethernet support
  CONFIG_NETDEVICES                                                                            Y          Network device support
  CONFIG_NET_VENDOR_3COM                                                                       Y          3COM Ethernet cards
  CONFIG_VORTEX                                                                                M          3c590/3c900 series (592/595/597) \"Vortex/Boomerang/Cyclone\" support
  Note: Vortex support has to be compiled modular because we have two NICs of the same type.              
  Sound options                                                                                           
  CONFIG_SOUND                                                                                 Y          Sound card support
  CONFIG_SOUND_OSS                                                                             Y or M     OSS sound modules
  CONFIG_SOUND_SB                                                                              Y or M     100% Sound Blaster compatibles (SB16/32/64, ESS, Jazz16) support
  CONFIG_SOUND_EMU10K1                                                                         Y or M     Creative SBLive! (EMU10K1) based PCI sound cards
  System self-monitoring options                                                                          
  CONFIG_I2C                                                                                   Y or M     I2C support (needed for SMBus)
  CONFIG_I2C_CHARDEV                                                                           Y or M     I2C device interface
  CONFIG_I2C_ALGOBIT                                                                           Y or M     Support for \`bit-banging\' I2C device
  Serial and Parallel ports                                                                               
  CONFIG_SERIAL                                                                                Y or M     RS232C serial-port support
  CONFIG_PARPORT                                                                               Y or M     Parallel-port support
  CONFIG_PARPORT_PC                                                                            Y or M     PC-style hardware
  CONFIG_PARPORT_PC_FIFO                                                                       Y          Use FIFO/DMA if available
  CONFIG_PARPORT_1284                                                                          Y          IEEE 1284 transfer modes
  Other device options                                                                                    
  CONFIG_BLK_DEV_FD                                                                            Y          Floppy disk support
  CONFIG_PSMOUSE                                                                               Y          PS/2 mouse (aka \"auxiliary device\") support
  CONFIG_RTC                                                                                   Y          Real-Time Clock support
:::

Now here is the patch for the Radeon timing bug:

+------------------------------------------------------------------------------------+
| ``` PROGRAMLISTING                                                                 |
| Index: radeon_driver.c                                                             |
| ===================================================================                |
| RCS file: /home/x-cvs/xc/programs/Xserver/hw/xfree86/drivers/ati/radeon_driver.c,v |
| retrieving revision 1.33                                                           |
| diff -u -r1.33 radeon_driver.c                                                     |
| --- radeon_driver.c 2001/08/07 07:04:43 1.33                                       |
| +++ radeon_driver.c 2001/08/09 23:00:20                                            |
| @@ -3588,6 +3588,7 @@                                                              |
|          OUTREG(RADEON_DAC_CNTL2, restore->dac2_cntl);                             |
|                                                                                    |
|      RADEONRestoreMode(pScrn, restore);                                            |
| +    usleep(100000);                                                               |
|      if(!info->IsSecondary)                                                        |
|      {                                                                             |
|      vgaHWUnlock(hwp);                                                             |
| ```                                                                                |
+------------------------------------------------------------------------------------+
::::::

::: NAVFOOTER

------------------------------------------------------------------------

  ----------------------------------------------------- ------------------------------------- -----------------------------------------------
  [\<\<\< Previous](horror_story.html){accesskey="P"}    [Home](ulb2001.html){accesskey="H"}    [Next \>\>\>](conclusion.html){accesskey="N"}
  The Inevitable Horror Story                                                                                                      Conclusion
  ----------------------------------------------------- ------------------------------------- -----------------------------------------------
:::
