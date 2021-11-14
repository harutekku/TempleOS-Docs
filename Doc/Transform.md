# Transform
`CDC`[^1]'s have a 4x4 matrix for rotating, scaling, skewing and shifting in 3 dimensions. To make the graphics routines use the transform, you must set the `DCF_TRANSFORMATION`[^2] flag.

The matrix consists of ints that have been scaled 32 bits (`GR_SCALE`[^3]). See [FixedPoint.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/FixedPoint.HC) to learn why.

See `Mat4x4IdentEqu()`, `Mat4x4IdentNew()`, `Mat4x4Equ()` and `Mat4x4New()`. See `Mat4x4RotX()`, `Mat4x4RotY()`, `Mat4x4RotZ()` and `Mat4x4Scale()` to rotate about axes and scale. Combine them with `Mat4x4MulMat4x4Equ()`/`Mat4x4MulMat4x4New()` and assign them to the `CDC.dc`[^1] with `DCMat4x4Set()`. See [Box.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Box.HC).

You can rotate single points using `Mat4x4MulXYZ()`.

The 4th dimension allows a neat trick where you can place pos shifts (translations), into the matrix and `Mat4x4MulMat4x4Equ`/`Mat4x4MulMat4x4New` them to combine rotation/shift operations. Normally, you can't combine pos shift operations. See `Mat4x4TranslationEqu()` and [Transform.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Transform.HC).

Finally, `CDC`[^1]'s have an `x`, `y` and `z` which is an additional shift (translation).

The transformation is implemented as a callback on the `CDC`[^1]'s `transform()` member. The default `transform()` callback is `DCTransform()`. See [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC) or [CastleFrankenstein.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/CastleFrankenstein.HC) to see how to change the `transform()` callback for foreshortening.

[^1]: See MN:CDC

[^2]: See MN:DCF_TRANSFORMATION

[^3]: See MN:GR_SCALE
