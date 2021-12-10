# Assembler

See [Op Codes](https://github.com/cia-foundation/TempleOS/blob/archive/Compiler/OpCodes.DD) for opcodes. They're not standard. Some invalid insts are not flagged and some valid insts are not implemented. 16-bit asm support is limited.

Here are example inst formats:
```holyc
ADD	RAX,I64 FS:DISP[RSI+RDI*8]
ADD	RAX,I64 [DISP]
```
Current compiler output pos (inst ptr). Even works in HolyC expressions.

`$` works in `class`es.
```holyc
class MyFun {
    $ = -16;
    I64 local1;
    I64 local2;
    $ = $ + 256;
    I64 crazy;
};
```

## `LABEL:`
Defines an exported glbl label.

## `LABEL::`
Defines an non-exported glbl label.

## `@@LABEL:`
Defines a local label with scope valid between two global labels.

## `DU8`, `DU16`, `DU32`, `DU64`
Define BYTE, WORD, DWORD or QWORD. Can be used with `DUP()` and ASCII strings. For your convenience, the ASCII strings do not have terminating zeros. Define cmds must end with a semicolon.
<!--
## `USE16`, `USE32`, `USE64`

## `IMPORT` _sym1name_, _sym2name_;

## `LIST`, `NOLIST`
-->
## `ALIGN` _num_, `fill_byte`
Align to _num_ boundary and fill with `fill_byte`.

## `ORG` _num_
Set code addr for JIT or set module `Load()` addr -- has 16-byte `CBinFile`[^1] header and patch table trailing.

See [assembly language](./GuideLines.md) and [demo 1](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Asm/AsmAndC1.HC), [demo 2](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Asm/AsmAndC2.HC) and [demo 3](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Asm/AsmAndC3.HC).

[^1]: See MN:CBinFile
