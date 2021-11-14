# Graphics Overview
Dive into [Demo Index](./DemoIndex.md) to learn.

The order layers are drawn on top of each other is:

See `GrUpdateScrn()`, `GrUpdateTasks()` and `GrUpdateTaskWin()` called by the WinMgr task 30fps. Notice the task's [`draw_it()`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Gr/GrScrn.HC) callback being called. Only tasks on Core0 are allowed to have windows. There is one window per task, no child windows. You can have pop-up child tasks.

`CDC`[^1]s (device contexts) are a data type for controlling graphics on the scrn or graphics in mem. The device context structure has thick and color. You use `DCAlias()` to create your own structure, with its own color and thick. Free it with `DCDel()` when finished.

`gr.dc` is a device context for persistent data on the scrn, not needing to be redrawn. You create an alias for this by using `DCAlias()` and work with that. See [NetOfDots.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/NetOfDots.HC).

There are various flavors of line and point plotting routines. `GrLine()` and `GrPlot()` are the simplest. The others allow 3D graphics and rotations.

See [Transform](./Transform.md) for adding a transformation.

You change the `Fs->draw_it` var to point to your `DrawIt()` function which gets called each scrn refresh (30 fps). You draw everything in the window over and over again. See [Box.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Box.HC).

Use the graphic sprite resource editor, `<CTRL-r>`, to create a sprite that can be plotted with `Sprite3()` or output to the cmd line with `Sprite()`. Use `$IB,"",BI=1$` in a src program to insert the addr of sprite binary data item #1. To learn how the numbers work, after creating a sprite with `<CTRL-r>`, toggle to plain text with `<CTRL-t>` and check its num. Make an assignment to a ptr var or pass to `Sprite3()` with `$IB,"",BI=n$`. Use `<CTRL-r>`'s "Pointer to Sprite" to make a `$IB...$` entry. See [SpritePlot.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpritePlot.HC) and [SpritePlot3D.hc](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpritePlot3D.HC). The origin (zero point) for a sprite is defined by the cursor location when you pressed `<CTRL-r>` to make it. You can edit a sprite by clicking the cursor on it and pressing `<CTRL-r>` again.

Set `DCF_SYMMETRY`[^2] in the `CDC.flags`[^1] and call `DCSymmetrySet()` or `DCSymmetry3Set()`. This will plot a mirror image in addition to the primary image. Set `DCF_JUST_MIRROR`[^3] to plot just the image, but this required `DCF_SYMMETRY`[^2] to be set at the same time. Note: You can only have one symmetry active at a time including in `CSprite`[^4]s.

Use `DCNew()` to create a mem bitmap which can be used to work off-scrn and which can be GrBloted[^5] onto the scrn. If you set brush member of CDC to another CDC, all the graphic routines will `GrBlot()` the brush instead of `GrPlot()`. See [Blot.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Blot.HC).

There are a few raster operations[^6] available. They go in bits 8-11 of the `dc->color` member var which is a `CColorROPU32`[^7]. `ROP_COLLISION`[^8] is special. It counts the num of pixs drawn on non-background locations. Using `ROP_COLLISION`[^8] with vector `CSprite`[^4]'s is tricky because overlapping pixs from lines in the `CSprite` reg as collisions. You can either work with a nonzero count or convert your `CSprite` to a bitmap if your subelements draw on top of each other. Be sure to set `->bkcolor` before using `ROP_COLLISION`[^8]. See [Collision.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Collision.HC) and [Titanium.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Titanium/Titanium.HC).
 
The `->dither_probability_u16` member of `CDC`[^1] is a U16 used to statistically sel between two colors to get something resembling more shades of color. See [SunMoon.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SunMoon.HC) and [Shading.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Shading.HC). It works with many graphic routines, but not those with pens.

There is a mechanism built-in for generating motion based on differential equations, which allows realistic physics. You create an `CMathODE`[^9] struct with `ODENew()`, passing it the num of vars in the state vect. For realistic physics, you usually have 2 state vars for each dimension (for each mass) because motion is governed by F=mA which is a 2nd order equation. The two states are pos and velocity and to solve these you need to supply the derivative of pos and velocity. The derivative of pos is usually simply the current velocity and the derivative of velocity is the acceleration (the sum of forces on a mass divided by mass). To help provide meaningful names for values in the state vect, you can create an `COrder2D3`[^10] ptr and point it to a mass in the state vect. Six elements in the state vect are required for each mass.

See [CMathODeE](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Math/CMathODE)$.
See [Rocket.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Rocket.HC).

[^1]: See MN:CDC

[^2]: See MN:DCF_SYMMETRY

[^3]: See MN:DCF_JUST_MIRROR

[^4]: See MN:CSprite

[^5]: See MN:GrBlot

[^6]: See MN:ROP_EQU

[^7]: See MN:CColorROPU32

[^8]: See MN:ROP_COLLISION

[^9]: See MN:CMathODE

[^10]: See MN:Corder2D3
