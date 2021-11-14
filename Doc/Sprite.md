# Sprite
`CSprite`[^1] is an ordered list of these[^2] elements, created with `<CTRL-r>`. Normally, they are packed together in a list and the address of the first is passed to routines.

See [SpritePlot.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpritePlot.HC), [SpritePlot3D.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpritePlot3D.HC), [SpritePut.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpritePut.HC), [SpriteRaw.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpriteRaw.HC) and `SpriteMeshEd()`.

Be aware that copying `SP`, `IB`, or `IS` entries with the clip results in duplicate entries with different nums. You can manually remove dups by editing with `<CTRL-t>` and setting to the original num.

See [GrSpritePlot.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Gr/GrSpritePlot.HC) for how CSprite are stored.

[^1]: See MN:CSprite

[^2]: See MN:SPT_END
