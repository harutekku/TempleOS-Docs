# Credits

I, **Terry A. Davis**, wrote all of TempleOS over the past 13.9 years (full-time). It can run on some bare metal 64-bit PC's from about 2005-2010 with no layering, libraries, tools, modules or anything from other sources.  Otherwise, you run it in a virtual machine, like VMware, QEMU or VirtualBox. It is independent and stands alone. It has no networking, so it certainly doesn't call home. 100% of the src code is including on all distro's, from the kernel to the compiler to the boot loaders! It is public domain, not GPL.
  - [FontStd.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/FontStd.HC), is taken from [FreeDOS](http://www.freedos.org). It's public domain.
  - [FontCyryllic.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/FontCyrillic.HC), is taken from [OrientDisplay](http://www.orientdisplay.com/images/cyrillic-Russian-fonts.gif) without permission.
  - ATA Reg and Cmd Definitions[^1] are originally from Linux. Later, I got the spec.
  - The heap algorithm, [MallocFree.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Mem/MAllocFree.HC), is adapted from one I saw at Ticketmaster when I worked on their VAX operating system.
  - The LZW compression algorithm, [Compress.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Compress.HC), came from a magazine and I implemented it when I worked for Ticketmaster.
  - The adaptive-step-size-Runge-Kutta algorithm, [AMathODE.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/AMathODE.HC), is adapted from the book, "Numeric Recipies in C".
  - The mountain in some games is from http://www.public-domain-photos.com. The wolf in BlackDiamond is also from there. I took watermarked photos and converted to 16 color.
  - The FAT32 file system is owned by MicroSoft.
  - A few features were inspired by MATLAB, such as ans in expressions at the command-line. There is a lot of MSDOS, Windows, VAXTMOS (VAX Ticketmaster O.S.) and Unix inspiration, too, such as drive letters, command names, etc.
  - I included [PCIDevice Lst File](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/PCIDevices.DD) from http://www.pcidatabase.com/reports.php?type=tab-delimeted.
  - Thanks to whoever wrote this [CppHtml.HC.Z](http://web.archive.org/web/20100325153025/http://home.scarlet.be/zoetrope/cpphtml.htm). I'm a novice on web stuff and you helped me with html.  See [ToHTML.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/ToHtmlToTXTDemo/ToHtml.HC).
  - I looked at bootable CD boot sects, but didn't learn anything, finding it easier to make my own.
  - I think I got my original PC speaker code from Borland C.
  - I found PS/2 keyboard and mouse code on the net and documentation.  My code is very different.  I found VGA reg info on the net.
  - Thanks to http://www.osdev.org for a couple tips.
  - God told me to stick with 640x480 16 color and single-voice 8-bit signed MIDI-like sample for sound. He kept me from zombie-walking into making child windows like Windows. Instead, I made one window per task with no child windows. He also guided my progress, very obviously.
  - I got [Webster's Dictionary](http://www.templeos.org/files/DICTIONARY.DD) and [The King James Bible](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/Bible.TXT) from [Project Gutenberg](http://web.archive.org/web/20110730111436/http://promo.net/pg/).
  - John Carmack inspired me to use `Clamp`[^2] as a name instead of "Limit". He inspired me to use "needle" and "haystack" as names. He inspired me to simplify my Frames-Per-Second code.
  - Bill Gates inspired me to add comments to my [Help & Index](./HelpIndex.md).
  - I hired an artist, Cody Rigby, for $3,000 worth of pixel art.
  - Erik van der Karbargenbok wrote /Downloads shell scripts -- gw.
  - The random number generator is from Donald Knuth in the wikipedia entry for [Linear_congruential_generator](http://en.wikipedia.org/wiki/Linear_congruential_generator).

## Additional credits
  - _MSDOS_, _Windows_, _MovieMaker_, _MS Paint_ and _FAT32_ are trademarks owned by MicroSoft Corp.
  - _SiteBuilder_ is a trademark owned by Yahoo! Inc.
  - _MagicISO_ is a trademark owned by MagicISO Corp.
  - _MATLAB_ is a trademark owned by The Math Works, Inc.
  - [_FreeDOS_](http://www.freedos.org) is a trademark owned by Jim Hall.
  - _QEMU_ is a trademark owned by Fabrice Bellard.
  - _VAX_ is a trademark owned by Digital Equipment Corp.
  - _Linux_ is a trademark owned by Linus Torvalds.
  - _VAXTMOS_ is a trademark owned by Ticketmaster.

[^1]: See MN:ATA_NOP

[^2]: See MN:Clamp
