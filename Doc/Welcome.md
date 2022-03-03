# Welcome to TempleOS
## Introduction
TempleOS is a x86_64, multi-cored, non-preemptive multi-tasking, ring-0-only, single-address_mapped (identity-mapped), operating system for recreational programming. Paging is almost not used.

## Targeted audience
The people whom can most benefit are:
  - Professionals doing hobby projects
  - Teenagers doing projects
  - Non-professional, older-persons projects

## Goals
Simplicity is a goal to [keep the line count down](./Strategy.md), so it's easy to tinker with. As it turns-out, simplicity makes it faster in some ways, too. It never switches privilege levels, never changes address maps, tends to load whole contiguous files and other, similar things which boost speed. It's only 82,150 lines of code including the kernel, the 64-bit compiler, the graphics library and all the tools. More importantly, it's designed to keep the user's line count down -- you can do a [Hello World](./HelloWorld.hc) application in one line of code and can put graphics on the scrn with a three line program!

## Ideology
It's a kayak, not a Titanic -- it will crash if you do something wrong. You quickly reboot, however. DOS and the 8-bit home computers of the 80's worked fine without memory protection and most computers in the world -- the embedded ones -- operate without protection. The resulting simplicity of no protections is why TempleOS has value. In facts, that's the point of TempleOS. See the [TempleOS Charter](./Charter.md).

Conventional thinking is "failure is not an option" for general purpose operating systems. Since this OS is used in addition to Windows or Linux, however, failure is an option -- just use Windows or Linux if you can't do something. I cherry-pick what it will and won't do, to make it maximally beautiful. The following applications more or less form a basis that spans the range of use that TempleOS is intended for:
  - [BattleLines.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/BattleLines.HC)
  - [BigGuns.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/BigGuns.HC)
  - [BlackDiamond.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/BlackDiamond.HC)
  - [BomberGolf.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/BomberGolf.HC)
  - [CastleFrankenstein.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/CastleFrankenstein.HC)
  - [CharDemo.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/CharDemo.HC)
  - [CircleTrace.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/CircleTrace.HC)
  - [Collision.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Collision.HC)
  - [Digits.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Digits.HC)
  - [DunGen.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/DunGen.HC)
  - [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC)
  - [ElephantWalk.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/ElephantWalk.HC)
  - [FlapBat.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/FlapBat.HC)
  - [FlatTops.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/FlatTops.HC)
  - [Halogen.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Halogen.HC)
  - [MassSpring.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/MassSpring.HC)
  - [Maze.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Maze.HC)
  - [RainDrops.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/RainDrops.HC)
  - [RawHide.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/RawHide.HC)
  - [Rocket.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Rocket.HC)
  - [RocketScience.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/RocketScience.HC)
  - [Squirt.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Squirt.HC)
  - [TheDead.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/TheDead.HC)
  - [TicTacToe.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/TicTacToe.HC)
  - [TreeCheckers.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/TreeCheckers.HC)
  - [Varoom.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Varoom.HC)
  - [Wenceslas.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Wenceslas.HC)
  - [Whap.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Whap.HC)
  - [Zing.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Zing.HC)
  - [ZoneOut.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/ZoneOut.HC)
  - [childish.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/Examples/childish.HC)
  - [night.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/Examples/night.HC)
  - [prosper.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/Examples/prosper.HC)

## Technical topics
Two things to know about TempleOS are that tasks have `MAlloc()` and `Free()` heap memory, not applications, and tasks have compiler symbol tables that persist at a scope like environment variables in other operating systems, and the symbols can include functions.

For other operating systems, I hated learning one language for command line scripts and another for programming. With TempleOS, the command line feeds right into the [HolyC](./HolyC.md) compiler, line by line, and it places code into memory it `MAlloc()`s. The compiler is paused at the command line, waiting for input. Naturally, you `#include` a program to load it into memory and, usually, start it.

During the boot process, many files get [compiled](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC) before you have access to the command line. (Don't worry, booting takes only two seconds.) All the header declarations for the operating system are compiled and are available for use in your programs without needing to `#include` them. Everything is truly compiled to native [x86_64](http://en.wikipedia.org/wiki/Amd64#AMD64) machine code, **nothing is interpreted** and there is **no byte code**.

Statements at the global scope -- outside the scope of functions -- execute immediately. There is no `main()` function. Instead, you give meaningful names to what would be `main()` functions and you invoke them by calling them with a statement in the global scope, usually at the bottom of your file.

I started with C syntax, but didn't like the command line for a directory listing looking like this:

```c
Dir("\*.\*",FALSE);
```
So, I added default args from C++ and it looked like this:
```cpp
Dir();
```
I didn't like that, so I made parentheses optional on calls with no args and it, now, looks like this:
```holyc
Dir;
```
The syntax change created an ambiguity when specifying function addresses, like for calling `QSort()`. To resolve it, I  made a `&` required in front of function names when specifying an address of a function, which is better anyway.

Once I was no longer using standard C/C++ syntax, I decided to change everything I didn't like and call it [HolyC](./HolyC.md). Here are the new [operator precedence](./HolyC.md) rules.  It's Biblical! See Luke 5:37.

There are no object files in TempleOS and, normally, you don't make executable files either, but you can. That's known as [Ahead-of-Time](./Glossary.md) compilation. Instead, you [Just in Time](./Glossary.md) compile.

Tasks have no priority and are never removed from the queue. Instead, they often poll whatever they are waiting on and swap-out. (Swapping tasks takes half a microsecond and does not involve disk activity or memory maps.) See [Scheduler](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Sched.HC). Polling keeps it simple. It might be a problem if you had lots of tasks busy, which rarely happens on a home computer. The order of the tasks in the queue determines front-to-back window order.

The FAT32 filesystem is supported to makes exchanging files with a dual booted other operating system easy and there is the simple, 64-bit TempleOS [RedSea](./RedSea.md) filesystem. The [RedSea](./RedSea.md) has allocation bitmap for clus and all files are stored contiguously. You can't grow files.

TempleOS is geared toward reading and writing whole files. Since whole files are processed, compression is possible. Filenames ending in `.Z` are automatically compressed or uncompressed when stored and fetched. TempleOS does support direct block random access into files, however -- `FBlkRead()` and `FBlkWrite()`.

If a file is not found, `.Z` is added or removed and a search is done, again. There is no `PATH`, but parent directories are searched when a file is not found. This feature is especially useful for default account files.

The graphic resolution is poor, 640x480 16 color, but God said it was a covenant like circumcision. Also, that's all I feel comfortable with without GPU acceleration supported. A 1600x1200x24 bit scrn takes 37 times more memory, implying 37 times the CPU power. Also, a fixed size keeps it simple with everybody machine having the same appearance. Look on the bright-side -- you won't spend as much time twiddling pixels for your game art and you'll have tons of CPU power available, especially with multicore systems.

TempleOS is for hobbyist programmers on single user (at a time) home computers, not mainframes or servers. The focus task is all-important so symmetrical multiprocessing is almost pointless. Why does it matter running two apps at the same time twice as fast when you really want to run one faster?  You could say TempleOS does master/slave multiprocessing. The anticipated use for multicore is primarily putting graphics on the scrn. Hardware graphics acceleration is not used, so this is possible. See [TempleOS MultiCore](./MultiCore.md).

## Tasks
There is no distinction between the terms task, process or thread. All have a task record, `CTask`[^1], pointed to by the `FS` segment reg and are accessed with `Fs->` while `Gs->` points to a `CCPU`[^2] for the current CPU core. Each task can have just one window, but a task can have children with windows. (The segment regs are just used as extra regs -- there is nothing segmented about TempleOS' memory.) It is approximately the case that TempleOS is multi-threading, single-processing.

In TempleOS, [Adam Task](./Glossary.md) refers to the father of all tasks. He's never supposed to die. Since tasks inherit the symbols of parents, system-wide stuff is associated with Adam. His heap is like kernel memory in other operating systems. Since Adam is immortal, it's safe to alloc objects, not tied to any mortal task, from Adam's heap. He stays in a server mode, taking requests, so you can ask him to `#include` something, placing that code system-wide. A funny story is that originally I called it the root task and even had a `/Root` directory :-) Adam executes [StartOS.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC) at boot time.

## Startup
For easy back-ups, place everything you author in your `/Home` directory and subdirectories. Then, use `CopyTree()`. That should make upgrading easy, too. Customizable start-up scripts go in your `/Home` directory. The default start-up scripts are in the root directory. Copy the start-up files you wish to customize into `/Home` and modify them. See [Home Files](./GuideLines.md). You can make your own distro that includes everything and is a bootable live CD with [DoDistro.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/DoDistro.HC).

## Usage
Typically, your usage pattern through the day will be repeatedly left or right clicking on filenames in a cmd line `Dir()` listing. You left-click files to edit them and right-click to `#include` them. To begin a project, type `Ed("filename");`, supplying a filename. You can also run programs with `<F5>` when in the editor. `<ESC>` to save and exit the file. You'll need to do a new `Dir()` cmd, periodically, so make a macro on your PersonalMenu. Access your PersonalMenu by pressing `<CTRL-m>`, cursoring until you are on top of it and pressing `<SPACE>`.

Common shortcuts:
  - `<CTRL-t>` - toggles plain text mode, showing format commands, a little like viewing html code.
  - `<CTRL-l>` - inserts a text widgets.
  - `<CTRL-r>` - inserts or edit a graphic sprite resource at cursor location.
  - `<CTRL-d>` - brings-up the file manager. It's pretty crappy. I find I don't need it very often, believe it or not.
  - `<CTRL-b>` - toggles window border.
  - `<ALT-m>` - maximizes a window.
  - `<ALT-SHIFT-a>` - closes AutoComplete.
  - `<ALT-a>` - brings back AutoComplete.
  - `<ALT-v>` - vertically tiles windows.
  - `<ALT-h>` - horizontally tiles windows.
  - `<CTRL-ALT-t>` - new terminal window.
  - `<CTRL-ALT-n>` - switches to the next window.
  - `<CTRL-ALT-x>` - kills a window.
The ALT keys are defined in `~/HomeKeyPlugIns.HC`. You can customize them.

## Utilities
`Find()` is your best friend. There's a wrapper function called `F()` in your `~/HomeWrappers.HC.Z` file. Feel free to make wrapper functions for functions you use often and customize the args. By the way, `Find()` or `R()` can be used to replace strings across multiple files. You can access `Find()` using `<CTRL-SHIFT-f>`.

As you browse code, use the AutoComplete window to look-up functions, etc. `<CTRL-SHIFT-F1>` (or whatever number) to follow a sym to it's source. You can browse deeper and deeper. You go back with `<SHIFT-ESC>`.

Use the [Help & Index](./HelpIndex.md) or [Demo Index](./DemoIndex.md) to find-out what exists. Press `<F1>` for help or use the links on your menu (`<CTRL-m>`). Also, look in the `/Demo` or `/Apps` directories for inspiration.

Software is distributed as [RedSea](./RedSea.md) ISO files. Burn a CD/DVD, or set your CD/DVD in QEMU, VMware or VirtualBox to the ISO file. Then, access the 'T' drive. Or, `Mount()` the ISO.C file and access the 'M' drive in TempleOS. It must be a contiguous ISO.C file, so rename it under TempleOS to ISO.C.

Ideally, do not install applications such as games onto your hard drive because we wish to keep hard drive usage low, so the whole 'C' drive can be copied quickly to 'D'. Also, the `FileMgr()` `<CTRL-d>` starts too slowly when there are lots of hard drive files, but that is how we want it.

3rd party libraries are banned, since they circumvent the 100,000 line of code limit in the [TempleOS Charter](./Charter.md). All applications must only depend on the core TempleOS files and whatever they bring along in the ISO. This is similar to how Commodore 64 applications only depended on the ROM.

## Contact details
Create a [RedSea](./RedSea.md) ISO file with `RedSeaISO()`. Send an email to <tdavis@templeos.org> if you want me to post a link to your TempleOS code in the App Store.

# Credits
  - _Linux_ is a trademark owned by Linus Torvalds.
  - _Windows_ is a trademark owned by MicroSoft Corp.
  - _Commodore 64_ is a trademark owned by Polabe Holding NV.
  - _QEMU_ is a trademark owned by Fabrice Bellard.
  - _VMware_ is a trademark owned by VMware, Inc.
  - _VirtualBox_ is a trademark owned by Oracle.

[^1]: See MN:CTask

[^2]: See MN:CCPU
