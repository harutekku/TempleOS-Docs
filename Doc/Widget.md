# DolDoc Widget Help

[DolDoc](./DolDocOverview.md) is a TempleOS document type.

- `Expression` - a num or HolyC algebraic term with operators and HolyC syms can be entered.
- `Macro` - Most entries can behave like macro entries if you assign them macro strs.
- `InStr` - Like a macro except it is an [InFile](./Glossary.md). You can't have both an `in_str` and macro text defined. 

Tag Text is the text that will be displayed for the item. For links, you can leave it blank and the details of the link will be shown.
Hide means display nothing, making an entry invis.

## Positioning
- `Left X` - relative to the left margin.
- `Center X` - relative to the horizontal center of the window.
- `Right X` - relative to the right margin.
- `Top Y` - relative to the top of the window.
- `Center Y` - relative to the vertical center of the window.
- `Bottom Y` - relative to the bottom of the window.

## Effects
- `Blink` - make the text blink.
- `Invert` - make the text inverted.
- `Underline` - make the text underlined. 

## Scrolling and shifting
- `Scroll X Length [Expression]` - if a value is entered, the text will scroll in an area of this width.
- `Y Offset [Expression]` - if a value is entered, the text will be shifted vertically by this many pixs, so you can make superscripts or subscripts.
- `X Offset [Expression]` - if a value is entered, the text will be shifted horizontally by this many pixs.

## Tree
- `Tree` - The item will behave like a tree widget, with this as the root.
- `Collapsed` - The tree or hidden widget will begin collapsed.
- `Define Str` - will substitute a `#define` or `DefineLoad()` string for the tag.

## Quoting
- `Quote` - Make the res suitable for including in a program, in quotes, especially format entries in class definitions.

## Other
- `X [Expression]` - For cursor movements, the horizontal value.
- `Y [Expression]` - For cursor movements, the vertical value.
- `PopUp` - For macro's, run the macro in a PopUp window. Do this when making a macro to run a program, so it doesn't tie-up memory.
- `Escape` - For macro's, send an `<ESC>` char to exit before running the macro. Without this, the macro runs in the wrong window, usually.
- `Refresh` - Data  updates `$DA...$` entry continuously.
- `Html Link` - stores a link which will be embedded if you generate a html version of a document with [ToHTML.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/ToHtmlToTXTDemo/ToHtml.HC).
