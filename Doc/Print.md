# Print Fmt Strs

## Syntax
```
<fmt_arg> := %[-][0][<width>][.<decimals>][<flags>][h<aux_fmt_num>]<fmt_code>
```

See `StrPrintJoin()`.

### `<flags>`
  - `t` - truncate to `<width>`.
  - `,` - add commas every three digits or four nibbles.
  - `$` - makes `"Q"` convert `$` to `\x24`.
  - `/` - makes `"%Q"` and `"%q"` convert `%` to `%%`.

### `<aux_fmt_num>`

For `"%n"`, `"%d"` or `"%u"`, the `<aux_fmt_num>` causes thousands mode. `"%h?n"` will pick a var exponent multiples of three unit, while `"%h-3n"` will display milli units or `"%h6n"` will display mega units. The `k` flag is always on for `"%n"`. See [Print.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Print.HC).

For `"%c"` or `"%C"`, the `<aux_fmt_num>` repeats the char that many times.

### `<fmt_code>`
  - `"%n"` - floating point in engineering notation, exponents being multiples of three. If it has a <aux_fmt> code, it will display scientific units letters.
  - `"%S"` - `Define()` entry.
  - `"%C"` - `ToUpper()` character.
  - `"%h25c",'\n';` - 25 new-lines.
  - `"%h\*c",25,'\n';` - 25 new-lines.
  - `"%F"` - text file by filename.
  - `"%$F"` - [DolDoc](./DolDocOverview.md) file in memory.
  - `"%p"` - ptr. 
  - `"%,p"` - ptr with no offset. 
  - `"%P"` - link to ptr.
  - `"%,P"` - link to ptr with no offset.
  - `"%D"` - date. Pass a CDate[^1].
  - `"%T"` - time. Pass a CDate[^1].
  - `"%z"` - sub_entry of an enumerated list of text entries. See `LstSub()`. Pass sub_entry_num first, list second.
  - `"%Z"` - `DefineLstLoad()` subentry. Pass sub_entry_num first, define_name second.
  - `"%Q"` - convert `"\"` to `"\\\\"` and quote to backslash quote. (For use in creating strs in strs.)
  - `"%q"` - rev a `"%Q"`.

## Print Family
`MAlloc()`ated str. It is vary handy because you don't have to worry about overflow.

  - `CatPrint(U8 *_dst,U8 *fmt,...)` - concatenates a formated string.
  - `In(U8 *fmt,...)` - sends text to the current task's input buffer.
  - `InStr(U8 *fmt,...)` - sends text of an [InFile](./Glossary.md) to the keyboard stream of the current TASK but can also do mouse cmds.
  - `XTalk(CTask *task,U8 *fmt,...)` - and text to another task's input buffer.
  - `XTalkStr(CTask *task,U8 *fmt,...)` - sends text of an [InFile](./Glossary.md) to the keyboard stream of another TASK but can also do mouse cmds.
  - `DocPrint(CDoc *doc,U8 *fmt,...)` - sends text to a document. You can buffer to a Doc and save it, providing the functionality of fprintf. See [FPrintF.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Dsk/FPrintF.HC).
  - `Adam(U8 *fmt,...)` - sends text to the [Adam Task](./Glossary.md) to be compiled and run.
  - `AdamErr(U8 *fmt,...)` - send text to the [Adam Task](./Glossary.md) to be displayed.
  - `StreamPrint(U8 *fmt,...)` - sends text to the stream of code being compiled and must reside in a `#exe{ }` blk.
  - `GrVPrint()` - plots text in graphics mode.
  - `TextPrint(CTask *task, I64 x, I64 y, I64 attr, U8 *fmt, ...)` - plots to `gr.text_base` Textbase Layer.
  - `ExePrint(U8 *fmt,...)` - compiles and execute a string. Note: It returns the res of the last executed expression.
  - `Once(U8 *fmt,...)` - Writes User code to Registry[^2] to be executed next boot.
  - `AOnce(U8 *fmt,...)` - Writes Adam code to Registry[^2] to be executed next boot.
  - `PutChars()`s one at a time with a delay.
  - `RawPrint(I64 mS,U8 *fmt,...)` - sends direct to scrn memory, bypassing window manager.
  - `User(U8 *fmt,...)` - Spawns a user and execute a string on start-up.
  - `PopUpPrint(U8 *fmt,...)` - compiles and execute a string in a pop-up win. Note: It returns the res of the last executed expression.
  - `PopUpViewPrint(U8 *fmt,...)` - creates a pop-up window and views text.

Note: Use `Print("%s",src)` if you need an unmodified string.

[^1]: See MN:CDate

[^2]: See FI:~/Registry.HC