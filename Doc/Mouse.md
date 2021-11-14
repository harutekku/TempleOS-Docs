# Mouse
`ms.pos.x`[^1] and `ms.pos.y`[^1] can be used to access the x and y coordinates of the mouse. They are relative to the scrn, not window. These can be used if you don't want to use msg passing. `ms.pos.z`[^1] is the wheel.

`ms.pos_text.x`[^2] and `ms.pos_text.y`[^2] are the text column and row. See [Maze.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Maze.HC).

See `CMsStateGlbls`[^2] and `CMsHardStateGlbls`[^3].

The hard designation, as in `ms_hard`, represents hardware layer items before the application of an abstraction layer.

```holyc

ms_hard.pos.x = ms_hard.prescale.x * ms_hard.scale.x * ms_grid.x_speed;

ms.presnap.x = ToI64(ms.scale.x * ms_hard.pos.x) + ms.offset.x;

if (ms_grid.snap)
    ms.pos.x = Trunc(ms.presnap.x / ms_grid.x) * ms_grid.x + ms_grid.x_offset;
else
    ms.pos.x = ms.presnap.x;

```

[^1]: See MN:ms

[^2]: See MN:CMsStateGlbls

[^3]: See MN:CMsHardStateGlbls
