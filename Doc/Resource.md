# Graphic Sprite Resource Help

A sprite is an ordered list of elements such as lines, rectangles, bitmaps and color changes. In a program's source code, you first **make a sprite** somewhere outside a function. Then, you **insert a pointer** to the sprite as an `*elems` arg when calling `Sprite()` or `Sprite3()`. See `Sprites`.

You can create a sprite macro on your [PersonalMenu.DD](~/PersonalMenu.DD) with a payload of [HolyC](./HolyC.md) source code to execute when it ESC's back to the cmd line. If you check "Pop-Up", it will spawn a new task and run the payload. A pop-up macro can be placed in any document.
