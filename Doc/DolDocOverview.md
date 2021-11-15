# DolDoc

## Overview
DolDoc is a TempleOS document type supported by DolDoc Routines[^1]. In a document, commands are bracketed with `$`s. Use `<CTRL-l>` to experiment inserting a command. Then, use `<CTRL-t>` to toggle to plain text to see it.

## Grammar
Here is the grammar:

```
<DolDocCmd> := $<TwoLetterCmd>[<FlagList>][,<ArgList>]$ | $ColorName$

<FlagList>  := +|- <FlagCode>[<FlagList>]

<ArgList>   := <ArgCode>=<ArgExpression>[,<ArgList>]
```

The format of DolDoc cmds is a two character code, +/-flags, a comma and args separated by commas. Some commands have mandatory args. Optional args are indicated with <[ArgCode](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocInit.HC)>=. A ColorName[^2] bracked by dollars, will change the foreground color.

See [Widget](./Widget.md), [Demo](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/DemoDoc.DD), and [DemoToHtmlToTxt](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/ToHtmlToTXTDemo/ToHtml.HC).

## Two Letter Command
### Text
Normally, text is not bracketed with `$`, but if you wish to specify flag attr, such as centering text, you can bracket them with `$` and enter flags such as `$FG,2$+CX$FG$`. You can't edit them normally if they are bracketed by `$` unless you toggle to plain text mode with `<CTRL-t>`.

Commands:
  - `CR` - Hard New Line
    - New lines are normally not bracketed with `$`.
  - `SR` -  Soft New Line
    - Word wrap uses temporary soft new lines. Users never place soft new lines.
  - `CU` Cursor pos
    - The cursor pos is stored as a ASCII#5 character and is not bracketed with `$`. Users normally do not enter cursor pos.
  - `TB` - Tab
    - Tabs are normally not bracketed with `$`, but are ASCII#9.
  - `CL` - Clear
    - Clear all prev entries except ones with hold(+H) flags. You might want `+H` on word wrap entries. Alternatively, you can use `DocClear()`.
  - `PB` - Page Break
    - Page break.
  - `PL` - Page Length
    - Page length.
  - `LM` - Left Margin
    - Left margin.
  - `RM` - Right Margin
    - Right margin.
  - `HD` - Header
    - Top margin.
  - `FO` - Footer
    - Bottom margin.
  - `ID` - Indent +/- num
    - Changes the indentation deeper if positive, or shallower if negative. It effects the behavior of trees.

#### Examples
  - `$ID,2$` - indents 2 columns.
### Text Colors
You place an expression(usually a color define--see color defines[^3]) to indicate which of the 16 colors to use. If you enter no num, color returns to the default.
  - `FD` - Default Foreground Color
  - `BD` - Default Background Color
  - `FG` - Foreground Color
  - `BG` - Background Color
#### Examples
`$FD,BLUE$` - will set the default foreground color to BLUE.

### Effects
  - `WW` - Word-wrap
    - Include a `1` or `0`.
    - `$WW,1$` - turns word-wrap on.
  - `UL` - Underline
    - Include a `1` or `0`.
    - `$UL,1$` - turns underline on.
  - `IV` - Invert
    - Include a `1` or `0`.
    - `$IV,1$` - turns invert on.
  - `BK` - Blink
    - Include a `1` or `0`.
    - `$BK,1$` - turns blink on.
  - `SX` - Shift X positions
    - Include a num from `-7` to `7`. Only foreground is shifted. Positive right.
    - `$SX,3$` - shifts characters 3 pixels right.
  - `SY` - Shift Y pos
    - Include a num from `-7` to `7`. Only foreground is shifted. Positive down.
    - `$SY,3$` - shifts characters 3 pixels down.

### Cursor movement
`CM` - Cursor Movement

This has two expressions, one for X offset and one for Y. You can remove one or the other with `-LE` or `-RE`.
The expressions are relative to the current cursor location, unless you make them relative to:
  - `LX` - left
  - `CX` - center
  - `RX` - right
  - `MRX` - margin relative
  - `TY` - top
  - `CY` - center
  - `BY` - bottom
  - `PRY` - page relative

See [CursorMove.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/CursorMove.HC).

### External resources

### Anchor
`AN` - Anchor

The `CDocEntry.aux_str`[^4] arg is used for the anchor. I don't use these very often, but they're good sometimes. 

### Link
`LK` - Link

The `CDocEntry.aux_str`[^4] arg is used for the link text. With no aux the tag becomes the link text, as in example 3.

See Link Types[^5].

### Examples
`<CTRL-t>` to see
```
$LK,"File link to HelpIndex.DD",A="::/Doc/HelpIndex.DD"$
$LK,"File link to HelpIndex.DD with link type file",A="FI:::/Doc/HelpIndex.DD"$
File link with same tag str.  $LK,"::/Doc/HelpIndex.DD"$
$LK,"File find link searching for 'Admin'",A="FF:::/Doc/HelpIndex.DD,Admin"$
$LK,"File find link searching for 5th 'CTRL'",A="FF:::/Kernel/KernelA.HH,CTRL:5"$
$LK,"Manual page link",A="MN:Print"$
$LK,"File line num link",A="FL:::/Kernel/KernelA.HH,200"$
$LK,"File anchor link -- <CTRL-t> to see anchor after you click",A="FA:::/Demo/DolDoc/DemoDoc.DD,MyLittleAnchor"$
$LK,"Bible Link",A="BF:Acts,2:3"$ The chapter:verse actually just does a text search.
$LK,"Help Index Link",A="HI:Doc"$.
$LK,"Address Link",A="AD:0x11000"$.
```
For in-memory document address links, see `SpriteEdText()`.

## Forms

### Button
`BT` - Bttn

See [MenuBttn.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/MenuBttn.HC).

### Data
`DA` - Data

Used for forms that prompt for data or just displaying a value. Use `<CTRL-l>` to help you generate the DolDoc command text you need in your [HolyC](./HolyC.md) `class` member's `format` meta-data for `DocForm()`. See [Form.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/Form.HC), [DataBase.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Dsk/DataBase.HC), and [DocWidgetWiz.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocWidgetWiz.HC).

If you are not using `DocForm()`, make a `$DA...$` statement with `DocPrint()` and fill-in the `Fs->data` addr. See [task_title](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocEd.HC).   

The default raw data type for the `$DA...$` command is `RT=I64`. `DocForm()` will automatically reset the raw type to the value from the [HolyC](./HolyC.md) `class` member's definition if you leave it set to the default. Or, if not using `DocForm()`, specify a raw data type of `I8`, `U8`, `I16`, `U16`, `I32`, `U32`, `I64`, `U64`, or `F64`. See `DocDataFmt()` and `DocDataScan()`.

The `CDocEntry.aux_str`[^4] arg is used for the print/scan format string.

The default field length is `LEN=64` characters. For `U8 arrays[]`,`DocForm()` will automatically reset the field length to the string length from the [HolyC](./HolyC.md) `class` member's definition. The length measures starting after the ':' in the "" format string.

The space after the first ':' in the format string marks the first valid cursor pos. See [Data Tag Width](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocPlain.HC).

### Check box
`CB` - Check Box

Used for forms.  Use `<CTRL-l>` to help you generate the DolDoc command text you need in your [HolyC](./HolyC.md) `class` member's `format` meta-data for `DocForm()`. See [Form.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/Form.HC) and `CEdFindText`[^6].

If you are not using `DocForm()` make a `$CB...$` statement with `DocPrint()` and fill-in the `Fs->data` addr. See [task_title](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocEd.HC).   

The default raw data type for the `$CB...$` command is `RT=I8` which is `Bool`. `DocForm()` will automatically reset the raw type to the value from the [HolyC](./HolyC.md) `class` member's definition if you leave it set to the default. Or, if not using `DocForm()`, specify a raw data type of `I8`, `U8`, `I16`, `U16`, `I32`, `U32`, `I64`, `U64`, or `F64`. See `DocDataFmt()` and `DocDataScan()`.

### List Widget
`LS` - List Widget

Used for forms that prompt for data. You must specify a define list, `D=""`. Use `<CTRL-l>` to help you generate the DolDoc command text you need in your [HolyC](./HolyC.md) `class` member's `format` meta-data for `DocForm()`. See [Form.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/Form.HC).

If you are not using `DocForm()`, make a `$LS...$` statement with `DocPrint()` and fill-in the data addr. See [task_title](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocEd.HC).   

The default raw data type for the `$LS...$` command is `RT=I64`. `DocForm()` will automatically reset the raw type to the value from the [HolyC](./HolyC.md) `class` member's definition if you leave it set to the default. Or, if not using `DocForm()`, specify a raw data type of `I8`, `U8`, `I16`, `U16`, `I32`, `U32`, `I64`, `U64`, or `F64`. See `DocDataFmt()` and `DocDataScan()`.

### Menu value
`MU` - Menu Value

A left expression arg, `LE=<Exp>`, will return a number when clicked with the left mouse.

See `PopUpRangeI64()`.

### Hex edit
`HX` - Hex Edit

See `DocD()`.

### Tree Widget
`TR` - Tree Widget

A tree widget is a branch in a collapsable tree. The domain of the branch extends from the first +indent until enough -indents bring it back to where it started. Tree's begin collapsed unless a `-C` flag is present.

You might want to use `DocPrintAtomic()`.

See [TreeDemo.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/TreeDemo.HC).

### Sprite
`SP` - Sprite

Insert a sprite into text with `<CTRL-r>`. The cursor location at the time you press `<CTRL-r>` is critical because the sprite will be offset from that location. This is important when adding images to programs. Numbers for sprites are automatically chosen because copying to and from the clip requires this. You can insert another sprite with the same image by hitting `<CTRL-t>` and manually adding a `$SP...$` entry with the same `BI=num`.

You can add a text tag to the `$SP...$` cmd by manually adding text into the `$SP...$` cmd, as in `$SP,"pic 2",BI=2$`. If you enter a tag of the form `"<1>"` then the number in the tag will be updated to match the `BI=number`.

### Binary
`IB` - Insert Binary

Tells the compiler to insert a pointer to some binary data stored after the end of text in the document. There is just one type of binary data in DOC's at this point -- sprites -- created with `<CTRL-r>`. They have a number associated with them. This number is automatically chosen, because copying to the clip-board and back requires renuming. To use a `$IB...$` cmd, toggle to plain text (`<CTRL-t>`) after inserting a sprite and check the number in the `$SP...$` cmd. Create a `$IB...$` cmd with the same `BI=number` and the sprite will be inserted into the compiled stream like a string const.

You can, optionally, include tag text to be displayed for the `$IB...$` cmd. If you set the tag to `"<1>"`, then the editor will automatically update the tag if the `$BI=number` changes.

The reason for the `$IB...$` cmd is to pass a arg to `Sprite()` and `Sprite3()`. See [SpritePlot.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpritePlot.HC).

### Binary size
`IS` - Insert Binary Size

Inserts a number into the compiled stream describing the size of binary data associated with a bin number. I never use this.

### Song
`SO` - Song

See `Play()`. `CDocEntry.aux_str`[^4] stores the song note text.

### Highlihgt
`HL` - Highlighting

Include a `1` or `0`.

#### Examples
`$HL,1$` - will turn syntax highlighting on.

## Macro
`MA` - Macro

A left macro arg, `LM=""`, will send text when the left mouse is clicked.

A left in string, `+LIS`, flag will cause text to be sent to `InStr()` instead of `In()`. An InStr runs code. Literal text is in quotes and messages are sent with `Msg()`. See [InFile](https://github.com/cia-foundation/TempleOS/tree/archive/Demo/InFile).

Macro's are usually in your [PersonalMenu.DD](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/PersonalMenu.DD) and have the `+X` flag set by default. Adding `-X` prevents the usual `<ESC>` from being sent (which exits the PersonalMenu scrn). Note: When you click a macro on the cmd line, it will go to the bottom and execute unless you cancel the `<ESC>` with a `-X`.

## HTML
`HC` - html

See [ToHTML.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/ToHtmlToTXTDemo/ToHtml.HC) to generate a html version of a document. You can cause html code to be injected with `HC`. Use the `+HTML` flag to inject a html link.

## Error
`ER` - Error

When errors are detected in DolDoc cmds, an `ER` entry is generated.

## Flag Codes
`<FlagCode>` - See `Flag Defines` and [simple flags](./Widget.md).
  - `+H` - Hold
    - Causes not to delete this cmd when cleared with `CL` or when the `doc->max_entries` is exceeded. Word wrap is a good to hold. There is no way to delete these entries, at this point.
  - `+L` - Link
    - Make a cmd behave as a link. Perhaps, use this on a `$SP...$` cmd.
  - `+TR` - Tree
    - Make a cmd behave as a tree branch. Usually, this is placed on a `TX` entry. The tree extends from the start until another tree entry or when indentation has been expanded and reduced back to the starting value. A `+C` flag on a tree will start it collapsed.
  - `+LS` - List
    - Make a cmd behave as a list widget. See above. Usually, this is placed on a `TX` entry.
  - `+PU` - PopUp
    - A PopUp flag on a `MA` will cause the cmds to run in a new task, a pop-up window.
  - `+C` - Collapsed
    - A collapsed flag on a `TR` entry will cause it to start collapsed. A `-C` flag will make it start open.
  - `+X` - `<ESC>` (Exit)
    - The exit flag will cause a `$MA...$` macro to send an `<ESC>` before running to exit the PersonalMenu scrn and return to the cmd prompt. Actually, the default `$MA...$` has an exit flag set so you add a `-X` to turn-off `ESC`, for a `+PU` pop-up macro. If an entry is already at the cmd prompt, the `+X` will movement to the bottom of the window.
  - `+Q` - `<SHIFT-ESC>` (Abort Quit)
    - A quit flag is similar to a `+X` except a `<SHIFT-ESC>` instead of an `<ESC>` to exit.
  - `+Z` - Zero
    - A zero flag on a `HX` entry will cause the offset from zero. A `-X` will show the actual memory addr. By default, `HX` has the zero flag set.
  - `+RD` - Refresh Data
    - The Refresh Data flag on a `DA` or a `CB` makes the value on the scrn updated continuously.
  - `+UD` - Update Data
    - The Update Data flag on a `DA` or a `CB` makes the value in the `CDocEntry`[^4] updated when keys are typed on it.
  - `+TC` - Tag CallBack
    - See [CallBack.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/CallBack.HC).
  - `+LC` - Left CallBack
    - See [ClickCallBack.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/ClickCallBack.HC).
  - `+RC` - Right CallBack
    - See [ClickCallBack.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/CallBack.HC).

## Argument codes
`<ArgCode>` - See `Arg Defines`

### Tag string
`T=""` - Tag Str

Some cmds have a tag by default. See [TX+T](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocInit.HC). You can code `T="tag_text"` as just `"tag_text"` with no `T=`. 

### Field length
`LEN=""` - Field Length

The default field length for `$DA...$` commands is `LEN=64` characters. For `U8 arrays[]`, `DocForm()` will automatically reset the field length to the string length from the [HolyC](./HolyC.md) `class` member's definition. The length measures starting after the ':' in the format string.

The space after the first ':' in the format string marks the first valid cursor pos. See [Data Tag Width"](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/DolDoc/DocPlain.HC).

### Auxiliary string
`A=""` - Auxilliary Str

Some cmds need auxilliary strings. `str` means an `CDocEntry.aux_str`[^4] is present. `aux_str` is used for song note text, link text, anchor text, and `$DA...$` format string text.

### Define string
`D=""` - Define Str

A `D=""` means either a `define` str indirection is present on a text widget, or a define list is present on a list widget.

For indirection, the tag will be regenerated by substituting the value of a system `#define` or `DefineLoad()` string. See [DefineStr.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/DefineStr.HC), [ADefine.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/ADefine.HC) and [Memory Overview](./MemOverview.md).

For `LS` widgets, see [Form.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/Form.HC).

### HTML
`HTML=""`

See [ToHTML.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/ToHtmlToTXTDemo/ToHtml.HC) to generate a html version of a document. You can cause html link on an item with `HTML=""`.

### Left Expression
`LE=<Exp>` - Left Expression

Left expression. `CM` has this by default for X offset and you can leave-off the `LE=`, just putting the `<Exp>`.

See [MenuBttn.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/MenuBttn.HC).

### Left Macro String
`LM=""` - Left Macro Str

Left macro string.

### Right Expression
`RE=<Exp>` - Right Expression

Right expression. `CM` has this by default for Y offset and you can leave-off the `RE=`, just putting the `<Exp>`.

See [MenuBttn.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/MenuBttn.HC).

### Right Macro String
`RM=""` - Right Macro Str

Right macro string.

### Binary number
`BI=<Exp>` - Bin Number

Binary data item number.

### Binary pointer
`BP=""` - Bin Ptr

The BinPtrLink flags lets you specify a filename and bin num to import a bin.

#### Examples:
  - `$SP,"<tag>",BI=1,BP="filename,1"$` will import bin num "1" from filename.
  - `$SP,"<1>",BI=1,BP="::/Demo/Graphics/Mountain.HC.Z,Mountain"$` will import bin with tag name `Mountain` from `/Demo/Graphics/Mountain.HC.Z`.

### Raw data type
`RT=<raw_data_type>`

The default data-type for the `$DA...$` and `$LS...$` commands is `RT=I64`. If you do not specify a raw type and are using `DocForm()`, it will use the `class` member's raw type, automatically. The default for the `$CB...$` command is `RT=I8` which is `Bool`.

If not using `DocForm()`, change it to `I8`, `U8`, `I16`, `U16`, `I32`, `U32`, `I64`, `U64`, or `F64`. See `DocDataFmt()` and `DocDataScan()`.

### Shift X
`SX=<Exp>` - Shift X

Shift tag text `+/- 7` X pixels off the grid.

### Shift Y
`SY=<Exp>` - Shift Y

Shift tag text `+/- 7` Y pixels off the grid.

### Scroll X
`SCX=<Exp>` - Scroll X

Scroll text in a marquee of so many columns.

### User data
`U=<Exp>` - User Data

See [MenuBttn.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/MenuBttn.HC).

## Examples

`<CTRL-t>` to see how the following were done.
```
$UL,1$Underlined$UL,0$ $IV,1$Inverted$IV,0$ $BK,1$Blinking$BK,0$ $SY,-3$super$SY,0$ $SY,0$$SY,3$sub$SY,0$
$TX,"This is a big long scrolling msg.",SCX=10$
```
Cursor movements:
```
$CM+LX,LE=3,RE=3$Cursor moved 3 rows down and to 3rd column from left.
$CM+RX,LE=-40,RE=3$Note mandatory comma after flags
```
The following may be changed to modes instead of attr with flags.
```
$TX+CX,"This is centered"$
$TX+RX,"This is right justified"$
```

[^1]: See HI:DolDoc

[^2]: See MN:ST_COLORS

[^3]: See MN:BLACK

[^4]: See MN:CDocEntry

[^5]: See MN:LK_FILE

[^6]: See MN:CEdFindText
