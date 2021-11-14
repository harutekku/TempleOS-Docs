# InFiles
InFiles are used to generate user input to automate operations. The TempleOS tour is done with an InFile. It reminds me of a Unix pipe because StdOut of one gets chained into StdIn of another.

When an InFile runs, a child task is `Spawn()`ed which intercepts real user input and generates fake input. InFiles are [HolyC](./HolyC.md) programs run by the child whose stdout goes to the parent's input buffer. `Msg()` can be included in an InFile to send special keys or mouse cmds to the parent. While an InFile is running, the normal input gets diverted to the InFile task and can be filtered and sent back to the parent task. Unless you are driving functions which prompt for data, you can probably use an `#include` file in place of an InFile.

See [InDir.IN](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/InFile/InDir.IN).

Note: `In("")` can be used if all you need is to send ASCII characters. It differs from `InStr()`. You'll probably use `In()` a lot and not `InStr()`. With `In()`, for example, you can place answers to the prompts for recompiling the Kernel module during `BootHDIns()`.
