# Guidelines
## Directory Structure

`/Home` - All your user data should be placed in here to ease backing-up your data. When you install an application it will create a subdirectory of your `/Home` directory for storage.

`/Apps` - Applications are placed in subdirectories of `/Apps`. Applications should have a file called `Install.HC.Z` which will install the app, possibly making files or directories in `/Home`. The file, `Load.HC.Z` will load the application into mem. The file, `Run.HC.Z`, will usually load and execute the app. To add an app to your PersonalMenu, use `<CTRL-l>`, insert a macro with the PopUp option checked and invoke the `Run.HC.Z` file.

`/Demo` - Here you can find lots of sample code to do various things.

`/Doc` - Here you can find documentation.

`/Kernel` - The core of the operating system is found here. Since priviledge levels are not used, calling it a kernel is deceptive. It is AOT compiled by `BootHDIns()`. It is loaded by the boot loader and must fit in 640K.

`/Compiler` - The compiler module src code is found here. The compiler is AOT compiled to produce a binary file which is loaded at boot. It, too, is AOT compiled by `BootHDIns()`.

`/Adam` - The non-kernel part of the operating system is found here. It is JIT compiled during boot. The [Adam Task](./Glossary.md) is the father of all tasks, like Adam and Eve.

`/0000Boot` - Boot files go here. Stage 2 of the TempleOS hard drive master boot loader, the old hard drive master boot record which is just blk#0, and the CD/DVD `0000Kernel.BIN.C` file go here. ASCII 0000 is near the top, alphabetically, in case you use [MagicISO](http://www.magiciso.com).

### `/Home` Files

The home dir is specified with `~`. The home dir is `::/Home` unless you change it with `HomeSet()` or compile the kernel with a cfg option. An empty `/Home` dir should be valid because it will get default files from the root dir. 

`~/PersonalMenu.DD` a menu viewed with the `<CTRL-m>` key or by clicking "MENU" in the upper left border area of a window.

`~/PersonalNotes.DD` a personal note file viewed with the `<CTRL-SHIFT-M>` key.

`~/MakeHome.HC` a file compiled by the [Adam Task](./Glossary.md) during [StartOS](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC).

`~/Home*` Copy `Home\*` files from the root into ~ and customize them. These files are invoked when the [Adam Task](./Glossary.md) starts-up.

`~/Once.HC` a file invoked at the start-up of the first user. Customize this!

`~/Registry.HC` can be edited by hand or deleted to reset to defaults. Takes affect next boot.



## Application Policies

Place applications in their own `/Apps` subdirectory.

Make a file called `Load.HC.Z` to load the application.

Make a file called `Run.HC.Z` to load and run the application, preferable by #includeing the `Load.HC.Z` file.

Place user data in a subdirectory of `/Home`, preferably naming the subdirectory the same as the `/Apps` subdirectory. Or, place data in the `Registry.HC.Z` file. See [RegistryDemo.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/RegistryDemo.HC).

If the app needs files in the `/Home` directory, make an `/Apps` file called `Install.HC.Z` or `Install.IN.Z` to create the `/Home` subdirectory.
 
## Programming Guidelines

Virtual mem/Paging is not used -- it is identity mapped in x86_64 mode. The stk does not grow, so alloc enough when the task (process) is Spawn[^1]ed and use the heap for most things. (The heap refers to `MAlloc()` and `Free()`.)

You can `Free(NULL)`.

See [Naming Convention](./Glossary.md) and [Abbreviations](./Glossary.md).

There are two modes of compiling, [AOT Compile Mode](./Glossary.md) and [JIT Compile Mode](./Glossary.md). Compilation is done in both -- neither is "interpreted". Use [JIT Mode](./Glossary.md).

[HolyC](./HolyC.md)

Use `I64` instead of smaller int sizes because the compiler converts everything to 64-bit. Don't use unsigned unless it actually breaks. A policy of signed keeps it simple so you don't have to agonize over choices.

```holyc
// This requires zero-extend when fetching args.
U32 DistDist(U16 x1, U16 y1, U16 x2, U16 y2) {
  return SqrI64(x1 - x2) + SqrI64(y1 - y2);
}

I64 DistDist(I64 x1, I64 y1, I64 x2, I64 y2) {
  return SqrI64(x1 - x2) + SqrI64(y1 - y2);
}
```
In-order, short circuit logic is assumed.

Avoid boolean expression assignments. Boolean assignments don't have short circuit logic and are not compiled efficiently. The Bool type is just an alias for a 1 byte signed int -- nothing forces it to 1 or 0. There is a `ToBool()` function that will for to 1 ot 0, however.

Glbl vars in AOT BIN modules are initialized to zero. They occupy space in BIN files.

Bracketing code with PUSHFD CLI and POPFD will protect against simultaneous accesses from tasks on *one* core. To protect against multiple cores, you need a locked semaphore. I think semiphores need to be in their own cache line, but I'm not sure. I use lock bits in a lot of places not aligned.

`SysDbg()` and `IsSysDbg()` are really handy when working on the compiler or kernel. It's just a bit you can set and test.

I don't use `U0*` because the size is zero for ptr arithmetic.

Use `CH_SHIFT_SPACE`[^2] for spaces in quotes in source code because I run [Spaces-to-Tabs](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Utils/StrUtils.HC) on source code.

Do not use `#if` or `#ifdef`

## Hash Sym Tables

See [Ahash.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/AHash.HC) for examples of how the hash tables are set-up. Basically, syms are placed into hash tables and child process hash tables are chained to parents. This provides scopes for vars and functions.

`adam_task->hash_table` holds the [HolyC](./HolyC.md) syms loaded in on start-up.

`Fs->hash_table` holds user HolyC syms and if a sym is not found, it checks parents. When a duplicate sym is added to the table, it overshadows the prev sym. When developing software, typically you include the file at the cmd prompt, make changes and reinclude it. Old syms are overshadowed but they are still there. Periodically, kill the TASK and start fresh when mem is low. If you wish your applications to free themselves instead of staying in mem, spawn or `PopUp()` a task to run the application and kill it when it's done.

To display the contents of a hash table, use the `Who()` routine or the varients. `HashDepthRep()` gives a histogram of how long the chains are, in case you wish to make hash table sizes bigger.

## Assembly Language

See [Asm](./Asm.md).

FS must always point to the cur `CTask`[^3].

GS must always point to the cur `CCPU`[^4].

Don't change the segment regs unless interrupts are off. It's hard to do, anyway. `SET_FS_BASE`[^5] and `SET_GS_BASE`[^6].

When interacting with [HolyC](./HolyC.md) compiled code, preserve RBP, RSI, RDI, R10-R15 because the compiler uses these for reg vars. You are free to clobber RAX, RBX, RCX, RDX, R8 and R9. See Compiler Reg Masks[^7], `PUSH_C_REGS`[^8] and `POP_C_REGS`[^9].

I recommend using the standard stk frame for functions because `Caller()` is used to display the call stk, such as for the wallpaper.
```holyc
PUSH    RBP
MOV     RBP,RSP
SUB     RSP,nnnn
// ...
LEAVE
RET
```

The args are removed from the stack with RET1 stmts.
```holyc
RET1	16	//remove two args
```
No args are passed in regs.

RAX holds function return values, of course.

## Credits
  - _MagicISO_ is a trademark owned by MagicISO Corp.

[^1]: See MN:Spawn

[^2]: See MN:CH_SHIFT_SPACe

[^3]: See MN:CTask

[^4]: See MN:CCPU

[^5]: See MN:SET_FS_BASE

[^6]: See MN:SET_GS_BASE

[^7]: See MN:REGG_LOCAL_VARS

[^8]: See MN:PUSH_C_REGS

[^9]: See MN:POP_C_REGS
