# Debugging Overview

You can enter the debugger with `Dbg()` or `<CTRL-ALT-d>`. You might enter the debugger through a fault. Enter `G()` or `G2()` to continue execution. Place a call to `Dbg()` in your code at fatal error points to enter the debugger. If you see a stk dump, record the label + offset and unassemble, `U()`. `U("_RIP");`

`U(&FunName + offset)` to unassemble mem or `Uf("FunName")` to unassemble a function. `U("_RIP" - 16);`

While debugging, you specify addresses of assembly routines with just the label, as in `_MALLOC + 0x20`. You specify [HolyC](./HolyC.md) function names with `&` before functions as in `&Print + 0x10`.

I use `progress1 - progress4` for debugging because they show on the wallpaper. They're just global int vars.

You can use `AdamLog()` to send text to the [Adam Task](./Glossary.md) window. It works like `Print()`. I never use that. Instead, I use `RawPrint()`.

`D()`, `DocD()`, `RawD()` to do 16 column hex dump mem with numbering from zero. With DocD[^1] the values are updated continually and you can alter mem by editing.

`Dm()`, `DocDm()`, `RawDm()` to do 16 column hex dump mem with addresses showing.

`Da()` to do one column address dump (for stk, etc.) with symbolic addresses.

`Dr()` dumps regs. You can display and modify regs in the debugger with var-like labels, \_RAX, \_RBX, etc.

`ClassRep()` and the dynamic version `ClassRepD()` can be used to dump structures.

`Prof()` and `ProfRep()` provide code profiling. See [InProfile.IN](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/InFile/InProfile.IN) (This is an [InFile](./Doc/Glossary.md))

Use `RawPrint()` to print debug info bypassing the window framework. You pass these routines a count in milliseconds for how long it should be displayed. You can use `Raw(TRUE)` to make all output bypass the window framework. The WinMgr runs on Core0 and will overwrite raw text from other cores when it updates the scrn.

Use `SysDbg()` to set a flag which you can read with `IsSysDbg()` when you wish to trigger some debug activity. It's just a handy simple flag, nothing fancy.

There are flags for various trace options that can help debugging when there are compiler bugs. Often, you place them in `#exe { }` blocks.

`Echo()` turns on or off raw data going into the lexical analyzer.

`Trace()` unassembles code generated from the HolyC compiler.

`PassTrace()` shows intermediate code coming-out after optimization. The bits ctrl which passes are displayed.

There is a heap check utility which can find leaks. Use `HeapLog()`, `HeapLogAddrRep()` and `HeapLogSizeRep()`. It's a really simple program which intercepts `MAlloc()` and `Free()`. You can customize the code to find other heap issues.

You can define hndlr functions for `<CTRL-ALT-letter>` keys with `CtrlAltCBSet()`. They operate either in a interrupt environment or in the window mgr when it queues kbd msgs. You can do `Raw()` output. `<CTRL-ALT-letter>` hndlrs take a `scan_code` as an arg.

If you recompile Kernel with `BootHDIns()`, you can set the MemInit, option to initialize memory to a value at boot, the HeapInit option to cause mem alloced off the heap to be initialized or VarInit option so both global and local vars will be initialized to a value, but global AOT variables are always zero if not initialized. Pick a non-zero value to discover uninitialized var bugs. You can set `sys_var_init_flag`[^2] and `sys_heap_init_flag`[^3] after booting.

[^1]: See MN:DocD

[^2]: See MN:sys_var_init_flag

[^3]: See MN:sys_heap_init_flag
