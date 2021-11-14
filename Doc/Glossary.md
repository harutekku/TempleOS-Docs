# Glossary

## Abbreviations
```
Abs    Absolute
AC     AutoComplete
Acct   Account
ACD    AutoComplete Dictionary
Addr   Address
Alloc  Allocate
Alt    Alternate
AOT    Ahead-of-Time
AP     ApplicationProcessor (Core1 - Core7)
Arg    Argument
Asm    Assemble, Assembler or Assembly
Attr   Attribute
Aux    Auxilliary
BG     Backround
Bin    Binary
Blk    Block
Bmp    BitMap
Bttn   Button
Buf    Buffer
Bwd    Backward
CB     Call-Back, Code Block
Cfg    Config
Chg    Change
Chk    Check
Clip   Clipboard
Clus   Cluster
Cmd    Command
Cmp    Compiler
Cnt    Count
Const  Consant
Cont   Continue
Ctrl   Control.  The ctrl key is indicated with "^" in documentation.
Cur    Current
Cvt    Convert
Dbg    Debug
Dbl    Double
DC     Device Context
Del    Delete
Desc   Descriptor, Description
Dev    Device
Dft    Default
Dir    Directory, Direction
Div    Divide
Doc    Document
Drv    Drive
Dsk    Disk
Dst    Destination
Ed     Edit, Editor
Elem   Element
Equ    Equal
Evt    Event
Exe    Execute
Ext    Extern, Extended, Extract
Feat   Feature
FG     Foreground
Fmt    Format
Fwd    Forward
FPS    Frames per Second, First Person Shooter
fp_    Function ptr
Fun    Function
Gen    Generate
Glbl   Global
Gr     Graphic
Hndlr  Handler
IDE    Integrated Drive Electronics, Integrated Development Environment
Id     Identification
Ident  Identifier, Identity, Identical
IDT    Interrupt Descriptor Table
Idx    Index
Init   Initialize
Ins    Insert, Install
Inst   Instruction
Int    Interrupt, Integer
Irq    Interrupt (Request)
JIT    Just-in-Time
Kbd    Keyboard
KD     Keyboard Device
Len    Length
Let    Letter
Lex    Lexical Analyser
Loc    Location, Lines of Code
Log    Logarithm, Logical
Lst    List
Man    Manual
Mem    Memory
Mgd    Managed
Mgr    Manager
Mid    Middle
Mon    Month
MP     MultiProcessor
Ms     Mouse
Msg    Message
Num    Number
Obj    Object
Occ    Occurrence
ODE    Ordinary Differential Equation
Opt    Option, Optimize
Paren  Parenthesis
Pix    Pixel
Pkg    Package
Poly   Polygon
Pos    Position
Pow    Power
Prec   Precedence
Prev   Previous
Pri    Primary
Prod   Product, Production
Prof   Profile, Profiler
Prs    Parse, Parser
Prt    Partition
FunSeg Program Section
Pt     Point
Ptr    Pointer
Que    Queue
Rand   Random
Ref    Reference
Reg    Register, Registry, Regular
Rem    Remove
Rep    Report, Repeat
Res    Result
Rev    Reverse, Reversed
Rqst   Request
Rst    Reset
Rot    Rotation
Rx     Receive
Sched  Sceduler
Scrn   Screen
Sec    Second, Secondary
Sect   Sector
Sel    Select, Selected
Seq    Sequence
Snd    Sound
SP     SingleProcessor
Src    Source
Srv    Servant
Stat   Status, Statistic
Std    Standard
Stk    Stack
Stmt   Statement
Str    String
Sym    Symbol
Sync   Synchronization
Sys    System
Tbl    Table
Term   Terminal
Tmp    Temporary
Tri    Triangle
Tx     Transmit
UAsm   Unassemble
Val    Value
Var    Variable
Vect   Vector
Vis    Visible
Vol    Volume
Win    Window
Wiz    Wizard
```

## Task/Process/Thread
There is no distinction between task, process or thread. The Fs segment reg is kept pointing to the current task's `CTask`[^1]. There is only one window per task, and only Core0 tasks can have windows. Each task has a code and data heap so memory is returned when it dies. Each task has a `Hash`[^2] symbol table.

Since there is not friendly disk sharing and all tasks have the same address map, it might be accurate to call TempleOS, "multi-thread/single-process". You run a single application process on Core0 and it can create threads on the same core or others. If you run multiple processes, it should be safe, but one process will wait until another completely finishes a long disk access.  

## Adam Task
This is Adam, as in Adam and Eve, the parent of all tasks. Adam is immortal. The adam task is created at start-up and appears in the small window at the top beneath the user terminal windows. Since the Adam task is immortal, on Adam's heap go all memory objects which you don't want destroyed by any single task's death. When created, Adam runs the file [StartOS.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC). When start-up is finished, the adam task enters a server mode where it accepts requests from other tasks. The `Adam("")` routine will make Adam compile and run text src code. `#include` stmts can be sent to `Adam("")`, creating system-wide code and data which are immortal.

## Seth Tasks
In the Bible, Seth is Adam and Eve's child. Each CPU core has an executive task called Seth that is immortal. The Adam task on Core0 is also its Seth task.

## Code and Data Heaps
TempleOS uses the asm CALL inst, exclusively, and that inst is limited to calling routines +/-2Gig from the current code location. To prevent out-of-range issues, I decided to separate code and data, placing all code within the lowest 2Gig of memory, addresses 00000000 - 7FFFFFFF.  The compiler and `Load()`er alloc memory from the code heap to store code and glbl vars, unless the compiler option `OPTf_GLBLS_ON_DATA_HEAP`[^3] is used. When programs call `MAlloc()` is from the data heap, which in not limited in size, except by physical RAM memory. You can alloc from any heap in any task at any time on any core, even making independent[^4] heaps.

## Parent, Child and PopUp Tasks
Often a task will `Spawn()` or `PopUp()` a task as a helper. The helper is known as a child Task, though you can `Spawn` a task and assign it a different parent... like Adam. Links are kept as to who's whose child, so when one task is `Kill()`ed the child helper tasks die, too. You can get a report of current system tasks with `TaskRep()`. There is just one window per task, so child tasks are needed for pop-ups.

## HolyC
[HolyC](./HolyC.md) is more than C and less than C++. It has the default args of C++ and uses class in place of struct. It uses U0,U8,U16,U32,I64 and I0,I8,I16,I32,I64 for signed and unsigned ints. It has different [operator precedence](./HolyC.md). It has PASCAL-like function calls with no parens, but requires an & when referring to function addresses.

## AOT Compile Mode
Ahead-of-Time compiling is conventional compilation mode. Do not use AOT, use JIT compiling.

In AOT mode, .PRJ files are compiled to .BIN files, skipping .OBJ files. After compiling, .BIN files are `Load()`ed.

There is no `main()` routine. Instead, stmts outside functions are automatically executed upon loading. There is no way to unload except by killing the task. To invoke AOT Compiled Mode, `Cmp()` is used.  The Kernel module and compiler are made in AOT compiled mode. See `BootHDIns()`  which calls `MakeAll()` where `/Kernel.BIN.C`, `/Kernel/Kernel.PRJ` and `/Compiler/Compiler.BIN`, `/Compiler/Compiler.PRJ` are created.

## JIT Compile Mode
In just-in-time mode, the compiler places code and data in memory alloced from the heap, incrementally, making them immediately ready for in-place execution. This mode is used during cmd line operations. When you `#include` a file, it is compiled function by function and code ends-up all over in the memory, at least in the first 2Gig of memory. The `ExeFile()` routine is the same as `#include` but can be used in programs. `ExePrint()` routine will compile and run a string.

## Compiler Intermediate Code
The compiler generates insts one step before making actual assembly (machine) language insts. This code is rev polish stack machine in nature and can be viewed with `PassTrace()`. The compiler does not interpret code, except in the process of optimization to make the final machine code. Assembly language output can be viewed when code is compiled with the `Trace()`, or, afterward, with `U()` or `Uf("")`.

## Drive/Partition

There is no distinction between drive or partition. They are specified with a single letter from A-Z.
  - `:` is the boot drive.
  - `~` is the home drive.

The letters are reserved for different uses.
  - A-B are RAM drives.
  - C-L are ATA hard drives.
  - M-P are ISO file read drives.
  - Q-S are ISO file write drives.
  - T-Z are ATAPI CD/DVD drives.

For commands taking a drive letter as an argument, char 0 is the current drive.
  - Bt, Bts, Btr, Btc, BEqu[^5]
  - Define[^6]
  - [DolDoc](./DolDocOverview.md)
  - Editor Link Types[^7]
  - [files_find_mask](./FileUtils.md)
  - Hash Table[^2]
  - InFile[^8]
  - Ona[^9]
  - Pag[^10]
  - [RedSea File System](./RedSea.md)
  - Sprite[^11]

## CLI, STI, PUSHFD, POPFD
These are x86 assembly insts.
  - `CLI` - disable interrupts.
  - `STI` - enable interrupts.
  - `PUSHFD` - pushes the CPU flags.
  - `POPFD` - pops the CPU flags.

## Filename Extention Types
  - `*.???.Z` - These files are automatically compressed or uncompresses files when read or written.
  - `*.???.C` - Contiguous files--NOT compressed.
  - `*.DD.Z; *.DD` - Text Files
  - `*.HC.Z; *.HC` - HolyC src files.  The default HolyC compiler type is .HC.Z.
  - `*.PRJ.Z; *.PRJ` - HolyC src files to be compiled AOT.
  - `*.HH.Z; *.HH` - HolyC src header files.
  - `*.MAP.Z; *.MAP` - Compiler "map" files
  - `*.BIN.Z; *.BIN.C; *.BIN` - Binary executable files, created by `Cmp()` and read by `Load()`.
  - `*.DATA.Z; *.DATA` - Data files
  - `*.ISO` - CD/DVD image file.
  - `*.IN.Z; *.IN` - InFile Basically a HolyC program whose stdout goes to the input of a task when `InFile()` is called.
  - `*.GR.Z; *.GR` - Graphics file

## File masks
  - FILEMASK_TXT
  - FILEMASK_SRC
  - FILEMASK_AOT
  - FILEMASK_JIT
  - FILEMASK_GR

## Naming Convention
Since there are no namespaces and I don't plan to implement name spaces, I highly recommend putting a 2-3 character module code prefix on syms. e.g. WS, Doc, Lex

### ALL_CAPS
Assembly Language labels are capitalized with underscores between words. So are #define's.

### \_ALL_CAPS
Asm routines which are [HolyC](./HolyC.md) callable must have a leading underscore.

### MixedCaps
[HolyC](./HolyC.md) Functions and class names are MixedCaps.

### lower_case
Local function vars and glbl vars are lower case. Class member names are also lower_case.

### \_lower_case
Function args which are outputs (passed as ptrs) have leading underscores. Also, args which have idently named local variable counterparts have leading underscores. 

### DOCf_\*
Flags bit nums instead of bit values are designated with a lower case f.

### DOCG_\*
Flag groups are designated with "G".

### Misc.
res is reserved for local variables that hold the function return val.

I used C++ like naming. I place New, Del, Init, Rst, ect. on the end of a function name instead of at the beginning. RstMusicSettings should be MusicSettingsRst.

## Fs
The CPU FS segment reg. This reg points to the current task's `CTask`[^1].

## Gs
The CPU GS segment reg. This reg points to the current core's `CCPU`[^12].

## Heap
Programs can dynamically request chunks of memory alloced from a heap using `MAlloc()`. They must `Free()` it when finished. Ptrs are used to refer to the chunk. The heap is dynamically alloced mem.

## Join
When two parts of a program have a common low-level routine, that routine is often labeled SomethingJoin.

## user_data
Many operating system structures have space set aside for you to store values. You are on your own managing these with multiple applications and libraries.

## Multicore Core0/CoreAP
Core0, has the [Adam Task](./Glossary.md), and it is the master. The application processors have an executive [Seth Tasks](./Glossary.md) and are the slave processors. Only Core0 tasks can have windows and can launch applications. Slave cores are used if the application explicitly `Spawns()` a task or `JobQue()` a job on them.

[^1]: See MN:CTask

[^2]: See HI:Hash

[^3]: See MN:OPTf_GLBLS_ON_DATA_HEAP

[^4]: See MN:MemPageAlloc

[^5]: See HI:Bit

[^6]: See HI:Define

[^7]: See MN:LK_FILE

[^8]: See HI:InFile

[^9]: See HI:Snd

[^10]: See HI:Memory/BlkPoll

[^11]: See HI:Graphics/Sprite

[^12]: See MN:CCPU
