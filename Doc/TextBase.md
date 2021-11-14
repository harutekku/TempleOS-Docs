# TextBase
`gr.text_base`[^1] must be updated 30fps in your `Fs->draw_it()` callback. You probably want `GrPrint()` or just `Print()`. The [DolDoc](./DolDocOverview.md) code takes care of plotting text to `gr.text_base`[^1].

Memory layout:
  - Bits 0-7 - 8-Bit ASCII Scrn Code
  - Bits 8-11 - Foreground color[^2]
  - Bits 12-15 - Background color[^2]
  - Bits 16-20 - Signed X pos shift val
  - Bits 21-25 - Signed Y pos shift val
  - Bit  28	- Blink[^3]
  - Bit  29	- Invert[^4] (Swap foreground and background)
  - Bit  30	- Sel[^5] (XOR colors with FF)
  - Bit  31	- Underline[^6]

`GrUpdateTaskWin()` calls `DocUpdateTaskDocs()` which calls `DocRecalc()` where the document text is plotted into `gr.text_base`[^1]. Then, `GrUpdateTextBG()` and `GrUpdateTextFG()` render the `gr.text_base`[^1] onto `gr.dc2`[^1], a raw graphic bitmap.

See [Maze.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Maze.HC).

[^1]: See MN:CGrGlbls

[^2]: See MN:BLACK

[^3]: See MN:ATTRF_BLIBK

[^4]: See MN:ATTRF_INVERT

[^5]: See MN:ATTRF_SEL

[^6]: See MN:ATTRF_UNDERLINE
