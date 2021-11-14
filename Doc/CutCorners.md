# Cut Corners

There are a few places where I cut corners in the interest of not junking-up code. This is part of the TempleOS mentality. I try not to let stupid legacy compatibility issues enter and junk-up TempleOS.
  - I made my type-casting operator post-fix because it makes the compiler way cleaner.
  - TempleOS does not figure-out FAT32 short name alias numbers. `FAT32DirNew()`. It can cause hard drive corruption, so I might have to do it. It would really take a lot of junky code for this hatefully, detestable, legacy issue. "Please don't make me ruin my beautiful shiny-new TempleOS with that!" I am also not enthused about FAT32 because it is in patent limbo. FAT32 might get removed from TempleOS. There is the [RedSea](./RedSea.md) 64-bit file system that works perfectly well. FAT32 is useful, however, because it assists in transferring between dual booted operating systems.
  - I changed the [asm opcodes](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Compiler/OpCodes.DD) names to remove the ambiguity between insts with different numbers of arguments, making my [assembler](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Compiler/Asm.HC) simpler and I did minimal 16-bit asm support, since 64-bit is what you should be using, unless you're doing a [boot loader](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootDVD.HC).
  - There are no user-controlled file-sharing locks. However, the drive and file system have locks and concurrent operations should be fine. 
  - A hidden window is never refreshed. Certain tasks are never done, therefore. During refresh, the entry count limit of the document buffer is, normally, checked and enforced. If you print to the command-line in a task whose window is covered, no limit on buffer exists and it will alloc memory for the document buffer until the system runs out of memory and crashes.
  - Even if a local function variable is declared less than 64 bits, the compiler does calculations with 64-bit.
  - [`Print()`](./Print.md) uses `StrPrintJoin()`. You cannot use vastly over-sized fields for `%f`.
  - `GrEllipse3()` is broken on transformations.
 
