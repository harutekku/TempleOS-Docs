# Frequently Asked Questions

## How come it is public domain, not GPL?
I, Terry A. Davis, wrote all of TempleOS over the past 13.8 years (full-time). It can run on some bare metal 64-bit PC's from about 2005-2010 with no layering, libraries, tools, modules or anything from other sources. Otherwise, you run it in a virtual machine, like VMware, QEMU or VirtualBox. It is independent and stands alone. It has no networking, so it certainly doesn't call home. 100% of the src code is including on all distro's, from the kernel to the compiler to the boot loaders! See [Credits](./Credits.md).

## Shouldn't it be GNU/TempleOS?
TempleOS executes no code not written by me at any time except for a few BIOS calls for configuration. I even wrote boot-loaders, so I do not need Grub. See [Credits](./Credits.md).

## Don't you use GNU's gcc?
TempleOS was written from scratch, starting with TASM long ago, launching from real-mode DOS. Now, there is no Linux or GNU or any other code in TempleOS. Yes, I wrote the compiler from scratch. See [Credits](.Credits.md).

## Why do you dual boot?
TempleOS is 100% independent -- it does not access the files of your primary operating system and TempleOS will work as the only operating system on your computer, but it has no networking. In your off hours, you will use your other operating system.

## It has links, so is it a browser?
TempleOS is an operating system, not a browser. TempleOS links[^1] are a special format and only link too local files and symbol source addresses.

## Where are the animated 3D icon GIFs?
3D [Sprites](./Sprite.md) are stored as a mesh of triangles. There are no GIF files. It rotates 3D sprite objects on the fly.

## If the compiler is JIT, isn't it an interpretor?
TempleOS compiles, doesn't interpret, and uses no byte code anywhere. I loosely use the word script sometimes, but it's actually compiled. The compiler's optimization[^2] code is actually where the compiler evaluates constants to simplify them, like every optimizing compiler.

## Are you a Creationist?
I am an evolutionist. Adam is a better term for the first father of all tasks than root was!

## Is `Bt()` in the code Bit Torrent?
`Bt()` is bit test, like the x86 inst, not bit torrent.

## Is `Fs->` in the code file system?
`Fs` is a segment reg, not file system. (`Fs`[^3] is kept pointing to the current task's record.) There is no memory segmentation. It is 64-bit and flat. FS and GS are used as general purpose regs, more or less.

## Is it Pascal?
TempleOS uses a dialect of C/C++ called [HolyC](./HolyC.md). It is not Pascal. I altered the syntax making parenthesis optional on function calls with no paramaters.

## Why doesn't Sleep() make my laptop hibernate?
`Sleep()` makes a program pause. It is not hibernation for a laptop.

## What is Yield() for in loops?
`Yield()` saves the current task's regs (context) and loads in the next task. In a loop waiting for disk IO, it executes `Yield()` which pegs the CPU load, yet the system is responsive.

## What is JIT Compiled Mode?
The term [JIT Compile Mode](./Glossary.md) means it compiles and executes code placed into mem, not stored on disk.

## Why do files end in `.Z`? Are they encrypted?
Files with names ending in `.Z` are individually compressed using [TempleOS Compression](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Compress.HC). They are not encrypted. `Copy()` or rename them with `Move()` to a name without `.Z` and they will be stored in an uncompressed form. See [TOSZ](./TOSZ.md) for Linux or Windows uncompress C/C++ code.

## Is it open source? How do I build it?
TempleOS is 100% open src. All the src code is included in the distro. Use `BootHDIns()` to compile the kernel and compiler. The rest is [JIT Compiled](./Glossary.md) during boot. See [StartOS.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC). 

## Where are object files? How do I link?
TempleOS does not use object files or a linker. [AOT Compile Mode](./Glossary.md) is used to directly create flat binary files, [Kernel.BIN.C](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Kernel.PRJ) and [Compiler.BIN](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Compiler/Compiler.PRJ) with no object files and linking. [JIT Compile Mode](./Glossary.md) place code in memory, ready to run, with no object files or linking. Linking is done when BIN modules are `Load()`ed.

## What is the FPS refresh rate?
The refresh rate is "(30000.0/1001) frames-per-second. That is how often TempleOS updates scrn mem. It is not syncronized to the hardware.

## How does a task own the speaker?
No task or application has a lock on the speaker so apps will interfere with each other.

## Why does it leak memory?
TempleOS allocs mem as more items are displayed in the window. Also, TempleOS allocs mem for code as it is compiled at the cmd line. If you `#include` a file twice, it allocs more mem for it. If you have a 50,000 line program with each line taking twenty bytes on a machine with 1 Gig, you could `#include` it a thousand times if it had no data or graphics and no other use of mem. If it bothers you, hit `<CTRL-ALT-x>` and `<CTRL-ALT-t>`, periodically, to kill and recreate the task. Use the pop-up flag on macros in your [PersonalMenu](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/PersonalMenu.DD) to spawn new tasks, run applications and free the applications when they are finished. Small mem chunks stick to the task when they are freed until it is killed. The only way to get in trouble is allocating multiple Meg chunks and freeing them. These can only be reused if the same size gets alloced again. Use `HeapLog()`, `HeapLogAddrRep()` and `HeapLogSizeRep()` to see who alloced mem and didn't free it. See [Memory Overview](./MemOverview.md).

## Why do I get a memory leak when editing big files?
The editor periodically takes a snap-shot of the document for UNDO and this looks like a memory leak.

## Why is it in text mode?
TempleOS runs in VGA 640x480 16 color graphics mode, not text mode. It changes to this mode with a [BIOS call](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KStart16.HC) while in real-mode before it switches to 64-bit mode. The text is drawn by hand[^4]. See [FontStd.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/FontStd.HC). If graphics mode fails, it falls-back on text mode. You can force text mode with an [kernel config](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KCfg.HC) option.

## Where is the kernel memory?
TempleOS identity-maps all memory, all the time. It is like paging is not used. There is no special kernel high half memory space. TempleOS is ring-0-only, so everything is kernel, even user programs. There is a special task called Adam and he doesn't die, so his heap never gets freed. That's as close to kernel memory as it gets. All code goes in the lowest 2Gig of addresses, known as the [Code Heap](./Glossary.md), so that the REL32 addressing mode can be used. See [Memory Overview](./MemOverview.md).

## Why does it run code from stack addresses?
TempleOS puts all code in the lowest 2Gig, known as the [Code Heap](./Glossary.md), so that the REL32 addressing mode can be used. TempleOS is 64-bit, but 2Gig is enough for code. It actually puts global variables there, too, but you can turn that off with `OPTf_GLBLS_ON_DATA_HEAP`[^5]. `MAlloc()` allocs higher memory.

## How does it SYSCALL?
TempleOS doesn't use software interrupts or SYSCALL insts because it never needs to change out of ring-0, even running user programs. Calls are always CALL REL32 insts.

## How do you fault-in stack?
The stack does not grow, so do not do deep recursion. In theory, memory gets fragmented, too.

## How do I set the PATH?
There is no PATH. You do not enter filenames at the command-line and expect them to run. You enter C-like code. [Get Started Here](./CmdLineOverview.md).

## How do I boot it with Grub?
If you use Grub, you chain-load like Windows. See [Boot](./Boot.md). You can use the TempleOS boot-loader. [Master-Boot-Loader-Stage1](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootMHD.HC), [Master-Boot-Loader-Stage2](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootMHD2.HC), [Partition-Boot-Loader](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootHD.HC), [CD-DVD-Boot-Loader](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootDVD.HC).

## How do I get Kernel.BIN to boot?
The boot-loaders must be patched by you running `BootHDIns()` or `BootMHDIns()`. Those will write the block address into the boot-loader because the boot-loaders do not navigate file systems to find the [Stage2](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KStart16.HC) if you relocate it.

## Why is there some 16-Bit code?
TempleOS is 64-bit. Like all PC operating systems, the boot-loader starts in 16-bit real-mode. TempleOS calls a few BIOS info routines, switches to VGA-640x480x4bit, switches to 32-bit, then, 64-bit mode. There is an odd thing called a [PCI BIOS](http://www.o3one.org/hwdocs/bios_doc/pci_bios_21.pdf) which is 32-bit used for PCI config space access. TempleOS calls [that](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/PCIBIOS.HC) a couple times. It must temporarily drop-out-of 64-bit mode for that and stop multi-tasking.

## Why are you pushing 32-bit values on the stack?
PUSH EAX : All stack operations in 64-bit mode are 64-bits.

## Why are you using 32-bit insts and not setting high 32-bits?
XOR EAX,EAX : Operations on 32-bit regs clear the high 32-bits.

## How do you use the FS and GS segment registers.
MOV RAX,FS:[RAX] : FS can be set with a WRMSR, but displacement is RIP relative, so it's tricky to use. FS is used for the current `CTask`[^6], GS for `CCPU`[^7].

## How do I set ORG for position of code?
The compiler creates pos independent code. Don't create code which is loaded at a fixed, specified location. Code in a BIN file is pos independent by virtue of a table in the BIN file for patching absolute addresses.

## How are symbols loaded?
Binary executable files have export syms which are loaded into the sym tables. The operating system Kernel has such an export table. In addition, some map files are processed to provide more information on syms -- src file links. This is how the `Man()`/AutoComplete feature can find src lines.

##Why doesn't assert work?
`#assert` might print a message at COMPILE time, not run time.

## Why doesn't C++ public work?
The word public in [HolyC](./HolyC.md) does very little except allow the [Help & Index](./HelpIndex.md) and `Who()` to exclude meaningless syms.

## How does the debugger do source debugging?
When compilation takes place, the structures used by the compiler stick around. Data on classes can be accessed. See `ClassRep()`.

## What are the ASCII 5 and ASCII 31 chars doing in my text files?
The cursor location is stored as an ASCII 5 in files. ASCII 31 is SHIFT-SPACE, a character which does not get converted to tabs by space-to-tabs, `S2T()`. The ASCII 28 is SHIFT-ESC. 

## Why is there garbage at the end of my text files?
Binary sprite data is stored beyond the terminating NULL in text files. Map files store debug src line addresses.

## Why are sprites so small?
Sprites can be stored as vector graphics so they might take shockingly little room. They can be converted to bitmaps.

## Why don't I need to recompile `/Adam` and `/Home` files?
If you change code in the `/Adam` or your `/Home` directory, you don't need to recompile, you just need to reboot because those directories get recompiled when you boot. It uses [JIT Compile Mode](./Glossary.md). There is no `.BIN` file for JIT compilation. See [StartOS.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC).

## Why does it finds files that aren't there?
If not found, `.Z` is added or removed from filename and a search is done again. If a file is still not found, the parent directories are searched for a file of the same name.

## Credits
  - _Windows_ is a trademark owned by MicroSoft Corp.
  - _Linux_ is a trademark owned by Linus Torvalds.
  - _QEMU_ is a trademark owned by Fabrice Bellard.
  - _VMware_ is a trademark owned by VMware, Inc.
  - _VirtualBox_ is a trademark owned by Oracle.

[^1]: See MN:LK_FILE

[^2]: See MN:OptPass012

[^3]: See MN:Fs

[^4]: See MN:GrUpdateText

[^5]: See MN:OPTf_GLBLS_ON_DATA_HEAP

[^6]: See MN:CTask

[^7]: See MN:CCPU
