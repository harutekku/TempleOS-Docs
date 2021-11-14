# Graphic controls
To create a TempleOS graphic ctrl, you define callback functions and insert a `CCtrl`[^1] structure in the `CTask`[^2] queue. See [Slider.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Slider.HC), [ScrollBars.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/ScrollBars.HC) and [WallPaper.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/WallPaper.HC). There is a template-code ctrl generator, if you press `<CTRL-SHIFT-L>`.

[^1]: See MN:CCtrl

[^2]: See MN:CTask