# Help

## Keyboard Ctrls
  - `<SPACE>` - Left-Click
  - `<ENTER>` - Right-Click
  - `<F1>` - Help
  - `<CTRL-m>` - Personal Menu
  - `<ESC>` - Save  & Exit
  - `<SHIFT-ESC>` - Abort & Exit
  - `<WINDOWS KEY>` - Pull-down Menu

Other keys: Key Map

## Mouse Ctrls
  - `Right-Click` - Right-click menu
  - `Left-Click` - Edit (view)
  - `Double-Left` - Save  & Exit
  - `Double-Right` - Abort & Exit
  - `Top of Scrn` - Pull-down menu

## Keyboard-Mouse Ctrls
  - `Ctrl-LeftDrag` - Grab-Scroll Window
  - `Ctrl-Right` - Null scrolling
  - `<CTRL-ALT-z>` - Zoom scrn on Mouse
  - `<CTRL-ALT-Z>` - Unzoom scrn on Mouse

## Files
  - [Welcome](./Welcome.md)
  - [About TempleOS](./AboutTempleOS.md)
  - [Command Line](./CmdLineOverview.md)
  - [Demo Index](./DemoIndex.md)
  - [Features](./Features.md)
  - [Requirements](./Requirements.md)
  - [Charter](./Charter.md)
  - [Strategic Decisions](./Strategy.md)
  - [F.A.Q.](./FAQ.md)
  - [Glossary](./Glossary.md)
  - [HolyC](./HolyC.md)
  - [Compiler Index](./CompilerOverview.md)
  - [Why Not More?](./WhyNotMore.md)
  - [Demands](./Demands.md)
  - [The Std TempleOS PC](./StdTempleOSPC.md)
    
## User Help

  - [Key Allocations](./KeyAlloc.md)
  - [`/Home` Files](./GuideLines.md)
  - [TOSZ Linux Utility](./TOSZ.md)
  - [Tips](./Tips.md)
  - [Quirks](./Quirks.md)
  - [Directory Structure](./GuideLines.md)

## DolDoc
[DolDoc](./DolDocOverview.md) is the TempleOS document type. The editor, compiler, assembler and whole operating system seamlessly handle DolDocs. Cmds like `Dir()` and `Find()` can output links to the cmd line.

## Burning CD/DVDs
Prepare a directory with the files you wish to burn.

Use `RedSeaISO()` to make an ISO image file.

Use `DVDImageWrite()` to burn an ISO file onto a CD or DVD.

See [Making a Distro ISO](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/DoDistro.HC).

## Admin Help
Use `Mount()` to mount disk drives, perhaps, if you are booted to a LiveCD.

You recompile the kernel with `BootHDIns()`, and specify which drives should be mounted at boot. See [DoDistro.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/DoDistro.HC).

## Installing
[Install](./Install.md)

`/StartOS.HC` the TempleOS equivalent of the AUTOEXEC.BAT. It is run at start-up by the [Adam Task](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KMain.HC).

## Programmer help
  - [Guidelines](./GuideLines.md)
  - [HolyC](./HolyC.md)
  - [Graphics](./GraphicsOverview.md)
  - [DolDoc Documents](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/FileRead.HC)
  - [Lectures/AndNotMod.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/AndNotMod.HC)
  - [Lectures/FixedPoint.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/FixedPoint.HC)
  - [Lectures/NegDisp.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/NegDisp.HC)
  - [Lectures/Optimization.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/Optimization.HC)
  - [Lectures/ScrnMemory.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/ScrnMemory.HC)
  - [Lectures/GraphicsCPULoad.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/GraphicsCPULoad.HC)
  - [Lectures/InterruptDemo.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/InterruptDemo.HC)

## System Programmer Help
  - [64BitAsmQuiz](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/64BitAsmQuiz.DD)
  - Hash Tables[^1]
  - [Disk Stack](./FileLowLevel.md)
  - [PCIInterrupts.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/PCIInterrupts.HC)
  - MemRep[^2]
  - [WallPaper](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/WallPaper.HC)
  - [Scheduler](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Sched.HC)
  - [DolDoc](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/MakeDoc.HC)
  - [MiniGrLib](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/MiniGrLib.HC)
  - [MiniCompiler](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/MiniCompiler.HC)
  - [Backend](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Compiler/BackLib.HC)

## Index
  - AutoComplete[^3]
  - Bit[^4]
  - Boot[^5]
  - Call[^6]
  - [Char Overview](./CharOverview.md)
  - Char Routines[^7]
  - Circular Queue[^8]
  - [Command Line Overview](./CmdLineOverview.md)
  - Cmd Line Routines[^9]
  - [Compiler Overview](./CompilerOverview.md)
  - Compiler Routines[^10]
  - Compression[^11]
  - Ctrls[^12]
  - Data Types[^13]
  - Data[^14]
  - [Debugging Overview](./DbgOverview.md)
  - Debugging Routines[^15]
  - Define[^16]
  - Devices[^17]
  - Disk[^18]
  - [Documentation Overview](./DolDocOverview.md)
  - Doc Routines[^19]
  - Exceptions[^20]
  - File[^21]
  - [File Utils](./FileUtils.md)
  - Frames[^22]
  - God[^23]
  - [Graphics Overview](./GraphicsOverview.md)
  - Graphics Routines[^24]
  - Hash[^25]
  - Help system[^26]
  - [HolyC](./HolyC.md)
  - InFile[^27]
  - Info[^28]
  - Install[^29]
  - I/O[^30]
  - Job[^31]
  - [Key Allocations](./KeyAlloc.md)
  - Keyboard devices[^32]
  - Link Types[^33]
  - Math[^34]
  - [Memory Overview](./MemOverview.md)
  - Memory Routines[^35]
  - Menus[^36]
  - Messages[^37]
  - Misc[^38]
  - Mouse[^39]
  - MultiCore[^40]
  - [OpCodes](./Compiler/OpCodes.md)
  - [Operator Precedences](./HolyC.md)
  - PCI[^41]
  - [Print("") Format Strings](./Print.md)
  - Processor[^42]
  - Profiler[^43]
  - [RedSea](./RedSea.md)
  - Registry[^44]
  - [Scan Codes](./CharOverview.md)
  - ScrnCast[^45]
  - Sound[^47]
  - Sprites[^48]
  - StdIn[^49]
  - StdOut[^50]
  - String[^51]
  - Task[^52]
  - TextBase Layer[^53]
  - Time[^54]
  - Training[^55]
  - [TOSZ](./TOSZ.md)
  - Utils[^56]
  - Windows[^57]

[^1]: See HI:Hash

[^2]: See MN:MemRep

[^3]: See HI:AutoComplete

[^4]: See HI:Bit

[^5]: See HI:Boot

[^6]: See HI:Call

[^7]: See HI:Char

[^8]: See HI:Data Types/Circular Queue

[^9]: See HI:Cmd Line (Typically)

[^10]: See HI:Compiler

[^11]: See HI:Compression

[^12]: See HI:Ctrls

[^13]: See HI:Data Types

[^14]: See HI:Date

[^15]: See HI:Debugging

[^16]: See HI:Define

[^17]: See HI:Devices

[^18]: See HI:File

[^19]: See HI:DolDoc

[^20]: See HI:Exceptions

[^21]: See HI:File

[^22]: See HI:Hash/Frame

[^23]: See HI:God

[^24]: See HI:Graphics

[^25]: See HI:Hash

[^26]: See HI:Help System

[^27]: See HI:InFile

[^28]: See HI:Info

[^29]: See HI:Install

[^30]: See HI:I/O

[^31]: See HI:Job

[^32]: See HI:Keyboard Devices

[^33]: See MN:LK_FILE

[^34]: See HI:Math

[^35]: See HI:Memory

[^36]: See HI:Menus

[^37]: See HI:Messages

[^38]: See HI:Misc

[^39]: See HI:Mouse

[^40]: See HI:MultiCore

[^41]: See HI:PCI

[^42]: See HI:Processor

[^43]: See HI:Profiler

[^44]: See HI:Registry

[^45]: See HI:ScrnCast

[^47]: See HI:Snd

[^48]: See HI:Sprites

[^49]: See HI:StdIn

[^50]: See HI:StdOut

[^51]: See HI:Char

[^52]: See HI:Task

[^53]: See HI:TextBase Layer

[^54]: See HI:Time

[^55]: See HI:Help System/Training

[^56]: See HI:Cmd Line (Typically)

[^57]: See HI:Windows
