# HolyC

See [Compiler Overview](./CompilerOverview.md).

See [Scoping and Linkage](./ScopingLinkage.md) for details on `extern`, `import`, `_extern`, `_import`, etc.

## Built-in types
Built-in types include `I0`, `I8`, `I16`, `I32`, `I64` for signed 0-8 byte ints and `U0`, `U8`, `U16`, `U32`, `U64` for unsigned 0-8 byte ints and `F64` for 8 byte floats.
```holyc
    U0     // void, but ZERO size!
    I8     // char
    U8     // unsigned char
    I16    // short
    U16    // unsigned short
    I32    // int
    U32    // unsigned int
    I64    // long (64-bit)
    U64    // unsigned long (64-bit)
    F64    // double
 // F32    // no float - not/implemented
```

### Type casting
Type casting is postfix. To typecast int or F64, use `ToI64()`, `ToBool()` or `ToF64()`. (TempleOS follows normal C float <--\> int conversion, but sometimes you want to override.  These functions are better than multiplying by "1.0" to convert to float.) 

### Type checking
No type-checking

### Escape characters
`$` is an escape character. Two dollar signs signify an ordinary `$`. See [DolDoc](./DolDocOverview.md). In asm or [HolyC](./HolyC.md) code, it also refers to the inst's address or the offset in a class definition. 

### Alternative initializers
A single quote can encompass multiple characters. `ABC` is equ to `0x434241`. `PutChars()` takes multiple characters.

```holyc
asm {
HELLO_WORLD::
    PUSH   RBP
    MOV    RBP,RSP
    MOV    RAX,'Hello '
    CALL   &PUT_CHARS
    MOV    RAX,'World\n'
    CALL   &PUT_CHARS
    LEAVE
    RET
}

Call(HELLO_WORLD);
PutChars('Hello ');
PutChars('World\n');
```

## Operators
### Comparison operators
Allows "5 < i < j + 1 < 20" instead of " 5 < i && i < j + 1 && j + 1 < 20".
```holyc
if (13<=age<20)
  "Teen-ager";
```
### Arithmetic operators
The `` ` `` operator raises a base to a power.

### Ternary operator
There is no question-colon operator.

### Operators precedence
TempleOS [operator precedence](/Compiler/CInit.HC_
```
  `, >>, <<
  *, /, %
  &
  ^
  |
  +, -
  <, >, <=, >=
  ==, !=
  &&
  ^^
  ||
  =, <<=, >>=, *=, /=, &=, |=, ^=, +=, -=
```

## Control statements
### `switch` statement
switch stmts always use a jump table. Don't use them with cases with really big, sparse ranges.

if you know a switch stmt will not exceed the lowest or highest case values. switch [] is a little faster because it doesn't check.

Allows ranges like "case 4...7:" in switch stmts. A no case number causes next higher int case in switch stmts. See [NullCase.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/NullCase.HC).

```holyc
I64 i;
for (i = 0; i < 20; i++) 
  switch (i) {
    case: "Zero\n";      break; //Starts at zero
    case: "One\n";       break; //One plus prev case.
    case: "Two\n";       break;
    case: "Three\n";     break;
    case 10: "Ten\n";    break;
    case: "Eleven\n";    break; //One plus prev case.
  }
```

### `sub_switch` statement
Switch statements can be nestled with a single switch expression! This is known as a "sub_switch" statement. `start` `end` are used to group cases. Don't goto out of, throw an exception out of, or return out of the start front porch area. See [SubSwitch.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/SubSwitch.HC).

```holyc
I64 i;
for (i=0;i<10;i++)
  switch (i) {
    case 0: "Zero ";    break;
    case 2: "Two ";     break;
    case 4: "Four ";    break;
    start:
      "[";
      case 1: "One";    break;
      case 3: "Three";  break;
      case 5: "Five";   break;
    end:
      "] ";
      break;
  }
// Ans: Zero [One] Two [Three] Four [Five]
```

### Looping constructs
There is no continue stmt. Use goto.

### Other
`lock { }` can be used to apply asm LOCK prefixes to code for safe multicore read-modify-write accesses. The code bracked with have LOCK asm prefix's applied to relevant insts within. It's a little shoddy. See [Lock.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/MultiCore/Lock.HC).

## Functions
### Entry point
There is no main() function. Any code outside of functions gets executed upon start-up, in order.

### Invocation
Function with no args, or just default args can be called without parentheses. 
```holyc
Dir("*");
Dir();
Dir;
```
### Default arguments
Default args don't have to be on the end. This code is valid:
```holyc
U0 Test(I64 i = 4, I64 j, I64 k =5 ) {
  Print("%X %X %X\n", i, j, k);
}

Test(,3);
```
### Function addresses
When dealing with function addresses such as for callbacks, precede the name with "&".

### Implicit `Print()` invocation
A char const all alone is sent to `PutChars()`. A string with or without args is sent to `Print()`. An empty string literal signals a variable fmt_str follows.
```c
void DemoC(char drv, char *fmt, char *name, int age) {
  printf("Hello World!\n");
  printf("%s age %d\n", name, age);
  printf(fmt, name, age);
  putchar(drv);
  putchar('*');
}
```
```holyc
U0 DemoHolyC(U8 drv, U8 *fmt, U8 *name, I64 age) {
  "Hello World!\n";
  "%s age %d\n",name,age;
  "" fmt,name,age;
  '' drv;
  '*';
}
```
### Variable argument count
Variable arg count functions (...) can access their args with built-in variables similar to 'this' in C++. They are 'I64 argc' and 'I64 argv[]'.  
```holyc
// Example I
I64 AddNums(...) {
  I64 i, res = 0;
  for (i = 0; i < argc; i++)
    res += argv[i];
  return res;
}

AddNums(1,2,3); // ans: 6

// Example II
public U0 GrPrint(CDC *dc, I64 x, I64 y, U8 *fmt, ...) {
  U8 *buf = StrPrintJoin(NULL, fmt, argc, argv);        // SPrintF() with MAlloc()ed string.
  GrPutS(dc, x, y, buf);                                // Plot string at x, y pixels. GrPutS is not public.
  Free(buf);
}

GrPrint(gr.dc, (GR_WIDTH - 10 * FONT_WIDTH) >> 1, (GR_HEIGHT - FONT_HEIGHT) >> 1, "Score: %4d", score);  //Print score in the center of the scrn.
```
### Function flags
`interrupt`, `haserrcode`, `public`, `argpop` or `noargpop` are function flags. See `IRQKbd()`.

## `struct`s, `class`es and `union`s

No typedef, use class.

class member vars can have meta data. format and data are two meta data types now used. All compiler structures are saved and you can access the compiler's info about classes and vars.  See [ClassMeta.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/ClassMeta.HC) and  `DocForm()`.

There is a keyword lastclass you use as a dft arg. It is set to the class name of the prev arg. See [LastClass.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/LastClass.HC), `ClassRep()`, `DocForm()` and [BlkDevRep.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Dsk/BlkDevRep.HC).

There are no bit fields, but there are bit access routines and you can access bytes or words within any int. See I64 declaration. A class can be accessed as a whole are subints, if you put a type in front of the class declaration.

union is more like a class, so you don't reference it with a union label after you define it. Some common unions are declared in KernelA.HH for 1, 2, 4 and 8 byte objects. If you place a type in front of a union declaration, that is the type when used by itself. See [SubIntAccess.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/SubIntAccess.HC). 

```holyc
public I64i union I64 {        //"I64i" is intrinsic. We are defining "I64".
  I8i i8[8];
  U8i u8[8];
  I16 i16[4];
  U16 u16[4];
  I32 i32[2];
  U32 u32[2];
};


I64 i = 0x123456780000DEF0;
i.u16[1] = 0x9ABC;
```
You can have multiple member vars of a class named "pad" or "reserved", and it won't issue warnings. 

Only one base class is allowed.

## Exception handling
See [Exceptions.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Exceptions.HC). `try { }` `catch { }` and throw are different from C++. `throw()` is a function with an 8-byte or less char arg. The char string passed in throw() can be accessed from within a `catch { }` using the `Fs->except_ch`. Within a `catch { }` blk, set the var `Fs->catch_except` to TRUE if you want to terminate the search for a hndlr.  Use `PutExcept()` as a hndlr, if you like.

## Warnings
A `no_warn` stmt will suppress an unused var warning.

## Registers
`noreg` or `reg` can be placed before a function local var name. You can, optionally, specify a reg after the `reg` keyword.

```holyc
U0 Main() {
  // Only use REGG_LOCAL_VARS or REGG_LOCAL_NON_PTR_VARS for reg vars or else clobbered.
  I64 reg R15 i = 5, noreg j = 4;
  no_warn i;
  asm {
    MOV    RAX,R15
    CALL   &PUT_HEX_U64
    MOV    RAX,'\n'
    CALL   &PUT_CHARS
    MOV    RAX,U64 &j[RBP]
    CALL   &PUT_HEX_U64
    MOV    RAX,'\n'
    CALL   &PUT_CHARS
  }
}
```

## Compiler options
You can use `Option(OPTf_WARN_PAREN, ON)` to find unnecessary parentheses in code.

You can use `Option(OPTf_WARN_DUP_TYPES, ON)` to find dup local var type stmts.

## PreProcessor directives
* With the `#exe { }` feature in your src code, you can place programs that insert text into the stream of code being compiled. [`#exe { }`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KMain.HC) for an example where the date/time and compile-time prompting for cfguration data is placed into a program. `StreamPrint()` places text into a src program stream following the conclusion of the `#exe { }` blk.

No `#define` functions exist (I'm not a fan)

Can't use <> with `#include`, use "".

## Memory management

A function is available similar to sizeof which provides the offset of a member of a class. It's called offset. You place the class name and member inside as in offset(classname.membername). It has nothing to do with 16-bit code. Both sizeof and offset only accept one level of member vars. That is, you can't do sizeof(classname.membername.submembername).

There is a function called `MSize()` which gives the size of an object alloced off the heap. For larger size allocations, the system rounds-up to a power of two, so `MSize()` lets you know the real size and you can take full advantage of it.

You CAN `Free()` a `NULL` ptr. Useful variants of `MAlloc()` can be found (`CAlloc`). Each task has a heap and you can MAlloc and Free off-of other task's heaps, or make an independent heap with `HeapCtrlInit()`. See `HeapLog()` for an example.

The stk does not grow because virtual mem is not used. I recommend allocating large local vars from the heap. You can change `MEM_DFT_STK` and recompile Kernel or request more when doing a `Spawn()`. You can use `CallStkGrow()`, but it's odd. See [StkGrow.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/StkGrow.HC). 

All values are extended to 64-bit when accessed. Intermediate calculations are done with 64-bit values.

```holyc
U0 Main() {
  I16 i1;
  I32 j1;
  j1 = i1 = 0x12345678;        //Resulting i1 is 0x5678 but j1 is 0x12345678

  I64 i2 = 0x8000000000000000;
  Print("%X\n", i2 >> 1);      //Res is 0xC000000000000000 as expected

  U64 u3 = 0x8000000000000000;
  Print("%X\n", u3 >> 1);      //Res is 0x4000000000000000 as expected

  I32 i4 = 0x80000000;         //const is loaded into a 64-bit reg var.
  Print("%X\n", i4 >> 1);      //Res is 0x40000000

  I32 i5=-0x80000000;
  Print("%X\n", i5 >> 1);      //Res is 0xFFFFFFFFC0000000
}
```
## Misc
`printf()` has new codes. See [`Print("")` Format Strings](./Print.md).

