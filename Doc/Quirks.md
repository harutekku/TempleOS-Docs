# Quirks

You run a risk of problems if you do file operations on the same files simultaneously because there is no file sharing/locking mechanism. Generally, the last write wins.

When using FAT32, TempleOS does not generate unique short-entry names, the ones with the `~s`. Not all FAT32 filenames are valid TempleOS names and it will complain. Do not access FAT32 drives not dedicated to TempleOS. Disable them with `DrvEnable(OFF)`, or they will generate error messages. FAT32 involves a long and short name for each file.

The stk does not grow because virtual mem is not used. I recommend allocating large local vars from the heap. You can change `MEM_DFT_STK`[^1] and recompile Kernel or request more when doing a `Spawn()`.

The syntax highlighting occassionally glitches. The compiler doesn't.

Call `DskChg()` when you insert a new removable media.

Accessing CD/DVD's is flacky. Try `Drv()` or `DskChg()` twice.

You can only extern something once. There is a varient called `_extern` which binds a HolyC definition to a asm sym. This, too, can only be done once.

A terminal task has a `CDoc`[^2] document structure that remains active even when you change `Fs->draw_it`. To prevent links in the `CDoc`[^2] from being activated when the user clicks in the window, do one of three things:
  - `DocBottom()` followed by `DocClear()` to clear the `CDoc`[^2] so it has no active widgets.
  - Disable window mgr bttn click checking with `Fs->win_inhibit` set to mask `WIF_SELF_MS_L | WIF_FOCUS_TASK_MS_L_D | WIF_SELF_MS_R | WIF_FOCUS_TASK_MS_R_D`. This inhibits window mgr operations but still generates messages from bttn clicks.

switch/case stmts alloc a single jump table--do not use with wide, sparse ranges of case values.

Don't do a `goto` out of a `try{ }`.

A goto label name must not match a global scope object's name. (It's not worth slowing-down the compiler to handle this case.)

`MemCpy()` only goes fwd.

A `Cd()` cmd must be followed by two semicolons if a `#include` is after it. This is because the preprocessor processes the next token ahead.

The assembler's error msgs are often off by a line and undefines are cryptic.

The last semicolon on the cmd line is converted to a dbl semicolon because the compiler looks ahead before doing a cmd. This normally has no negative effect, but when entering if stmts with else clauses it presents problems.

You can do a class fwd reference by using extern on the first declaration, but you can only do ptr references to the class.

When doing something like
```holyc
U0 Main() {
  U16 *_w = 0xA0000;
  *_w |= 0x8000;
}
```
The `|=` will be coded as a `U32` Bts inst resulting in a `U32` access instead of a `U16` access. This affects some hardware operations.

Compiler warning or error message line numbers will be off if you have a block of word-wrapped comments. You might press `<CTRL-t>` before doing an editor goto-line-number command.

[^1]: See MN:MEM_DFT_STK

[^2]: See MN:CDoc
