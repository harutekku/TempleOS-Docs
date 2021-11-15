# Define
TempleOS has a string indirection feature implemented with the same hash symbol table entry as `#define` macros, `HTT_DEFINE_STR`[^1]. Support for string lists is also provided, but it's not very efficient, though, you can make a hash table with a list using `HashDefineLstAdd()`. See [DocInit.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocInit.HC).

If you have an `@` as the first char of a define list entry, it is an alias for the prev entry num.

Each task can load its own Define strings. Remember, when a Hash[^2] table is searched for a string, if it is not found, the parent task's table is searched.

The [DolDoc](./DolDocOverview.md) framework supports text that changes based on entries in the task's symbol table. Set a text entry with a `D=` arg, as in `$TX,"",D="DD_MYSTRING"$`. See [DefineStr.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/DefineStr.HC), [ADefine.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/ADefine.HC) and [MemOverview](./MemOverview.md).

See [Define.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Define.HC).

[^1]: See MN:HTT_DEFINE_STR

[^2]: See HI:Hash
