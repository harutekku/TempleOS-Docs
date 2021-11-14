# TempleOS' Features
  - Oracle in with `<F7>` for words or `<SHIFT-F7>` for passages. See [tongues](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/God/HSNotes.DD).
  - x86_64, ring-0-only, single-address-map (identity), multitasking kernel with multicore support.
  - Master/Slave MultiCore 
  - Free, public domain, 100% open source.
  - No 32-bit krufty code.
  - 640x480 16 color VGA graphics.
  - Keyboard & Mouse support.
  - ATA PIO Hard drives, support for FAT32 and [RedSea](./RedSea.md) file systems with file compression.
  - ATAPI PIO CD/DVD support with RedSea file system. Can make bootable ISO files so you can roll-your-own distro's.
  - Partitioning[^1] tool, installer, boot loaders for CD/DVD and hard disk.
  - Editor/Browser for a new [Document Format](./DolDocOverview.md). Source files and the command line window can have graphics, links, icons, trees, colors, super/sub scripts, margins. Everything is seamless through-out the tool chain. No need for separate resource files.
  - 8-bit ASCII, not just 7-bit. Supported in entire tool chain. `<CTRL-ALT-a>`
  - Graphics in source code, no resource files, graphic sprite editor. `<CTRL-r>`
  - 64-bit pointers. All memory, even more than 4Gig, can be directly accessed by all tasks on all cores at all times.
  - Ring-0-only. Highest CPU privileged mode at all times. No off-limits insts. No time lost changing modes or address maps. Switches tasks in half a microsecond.
  - 2D/3D graphics library
  - Real-time fancy differential-equation solver for physics engines, to use in games. (Adaptive step-size Runge-Kutta, interpolated for real-time.)
  - Auto-completion, jump-to-source tool called AutoComplete with Dictionary.
  - Window Manager. Pan scrn with `<CTRL-LeftDrag>`. Zoom scrn on mouse cursor with `<CTRL-ALT-z>` / `<CTRL-ALT-SHIFT-Z>`.
  - File Manager, `<CTRL-d>`.
  - Code profiler[^2], merge[^3], diff[^4] utils.
  - PC Speaker support with many hymns.
  - Music composing tool.
  - Many games, [Demos](./DemoIndex.md) and [Documentation](./HelpIndex.md).
  - All source code included. Only compiles with the included TempleOS compiler and assembler.

[^1]: See MN:DskPrt

[^2]: See MN:Prof

[^3]: See MN:Merge

[^4]: See MN:Diff
