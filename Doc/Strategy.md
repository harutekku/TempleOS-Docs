# Decisions Making TempleOS Simple
## Ideology behind TempleOS
Everybody is obsessed, Jedi mind-tricked, by the notion that when you scale-up, it doesn't get bad, it gets worse. They automatically think things are going to get bigger. Guess what happens when you scale down? It doesn't get good, it gets better!

I limited it to 100,000 lines of code, forever! I never need a linker or make utility and I can use small labels.

People mock Bill Gates for, "640K should be enough." I say, "2Gig for code should be enough." The same people who mock Bill Gates are probably just like the black woman who sued for a trillion dollars.

My Dad worked on converting the Titan missile to the Gemini Mission rocket. It had to be "man-rated". You can bet that everything got an order of magnitude more complexity and documentation. My vision is a souped-up C64, not a 1970's mainframe; a kayak, not a Titanic.

Linux is a semi-tractor -- you need professional drivers for 20 gears. Linux has file permissions. Common people are hurt by file permissions.

Windows is a car.

TempleOS is a motorcycle -- if you lean-over too far, a motorcycle will crash. Don't do that! There are no side air bags on a motorcycle. DOS and C64 had no memory protections and ran in ring-0, with no security. This saves an order of magnitude complexity.

Linux and Windows are general purpose operating systems. They attempt to do any task you want. TempleOS cherry-picks tasks and is designed to do the same things a C64 did. This saves and order of magnitude complexity. For example, the [RedSea](./RedSea.md) file system allocates just contiguous files -- you load and save whole files at once. A benefit is this allows compression. Also, TempleOS does not do networking or multimedia. In theory, memory will fragment with lots of big files. The system would fall to pieces with multimedia, but God said 640x480 16 color is a permanent covenant like circumcision.

A three bttn mouse is like a leg you cannot put weight on. TempleOS just does hardware everybody has, with no divergent code bases for each machine's custom hardware. There is one graphics driver instead of 50 for different GPUs. This saves an order of magnitude complexity and makes for a delightful API, so developer's code is not like a frayed rope end.

## Design choices
  - Everything runs in kernel, ring 0, mode.
  - One memory map for all tasks on all cores with virtual addresses set equ to physical, just as though paging is not used.
  - One platform -- x86_64 PC's, no 32-bit support.
  - No security or cryptography.
  - No networking.
  - Least (greatest) common denominator hardware support. Mostly, one driver for each device class. I can't be in the business of different drivers. Compatibility is the greatest challenge for PC operating systems. Disk code does not use interrupts, avoiding compatibility risks. PS/2 keyboard/mouse is used instead of USB, also more compatible.
  - 640x480 16 colors. Updates whole scrn at 30 fps, optimized for full scrn games where InvalidRectangles are counter-productive.
  - One font, 8x8. Text and graphic layers done in software with text normally on an 8x8 grid. It can run in Text mode if graphic initialization fails.
  - Compiler extends all values to 64-bit when fetched and does only 64-bit computations intermediately. Assembler has minimal 16-bit support, good enough for compiling boot loaders.
  - No object files. Use JIT.
  - Whole files are processed almost exclusively, allowing compression.
  - [One language](./HolyC.md) and compiler for command-line, scripts, songs, automations and code.
  - One editor/word processor/browser for the command-line window, source code, documentation browser, dialog forms.
  - No child windows. One window per task. Bttns are widgets, not child windows. There are child tasks, however.
  - No distinction between thread, process or task.
  - The [Scheduler](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Sched.HC) is for home systems. It is not preemptiove. Disk requests are not broken-up, so sharing is bad. It's wonderfully simple.
  - [MultiCore](./MultiCore.md) is done master/slave, instead of SMP. Core0 applications explicitly assigns jobs. Locks are present allowing multicore file, heap, and hardware access, though.
  - Sound[^1] has single-voice 8-bit signed MIDI-like samples.
  - All tasks have a heap and a sym table. Scope is that of environment vars in other operating systems. As text is typed at the command line or you run programs by `#include`ing them, the syms go in the table. If a sym is not found, the parent task's table is checked. The father of all tasks has the API syms you'll need waiting in it's table. No need to `#include` headers.
  - No need for namespaces -- scoping occurs automatically based on task symbol table hierarchy with the [Adam Task](./Glossary.md)'s symbol system-wide global.
  - Sometimes, I [cut corners](./CutCorners.md) in the interest of keeping the code beautiful.

[^1]: See HI:Snd
