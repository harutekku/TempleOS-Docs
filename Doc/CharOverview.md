# Char Overview

A character is a single byte holding an ASCII code for a letter, num or sym. The TempleOS term is a `U8`.
Standard ASCII values range from 0 to 127. Values below 32 are ctrl key's. So, an ASCII #3 is a `<CTRL-c>`. TempleOS uses a few nonstandard values below 32. See Char Definitions[^1].

Examples:
  - ASCII #5  is the cursor location in a saved file.
  - ASCII #28 is `<SHIFT-ESC>`.
  - ASCII #31 is a `<SHIFT-SPACE>`.

TempleOS ASCII is 8-bit instead of 7-bit, so it also uses the range from 128-255. Press `<CTRL-ALT-a>` to see shapes for 128-255. Technically, `<CTRL-ALT-a>` are scrn codes[^2].

A key is typically specified with a scan code. TempleOS scan codes contain the key value in the lowest `U8`, and flags in the upper 3 bytes. See Scan Code Flags[^3] and Scan Codes[^4].

## Layout
TempleOS stores scan codes in 8 bytes.
  - `Byte 0` is the code.  NumPad keys, SHIFT, ALT, CTRL and GUI keys combined.
  - `Byte 1-3` are flags[^5].

The upper 4-bytes are copied from lower 4-bytes.
  - `Byte 4` is the code. Left, Right and NumPad keys distinct.
  - `Byte 5-7` are flags[^5].

## Example & additional information
Run the program [MsgLoop.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/MsgLoop.HC) to examine scan code. Press `<CTRL-SHIFT-l>` and "Insert ASCII/ScanCode".

See [Key Allocations](./KeyAlloc.md) and CKbdStateGlbls[^6].

A `String` is a bunch of ASCII characters terminated with a zero.

[^1]: See MN:CH_SHIFT_SPACE

[^2]: See HI:TextBase Layer

[^3]: See MN:SCF_CTRL

[^4]: See MN:SC_INS

[^5]: See MN:SCf_KEY_UP

[^6]: See MN:CKbdStateGlbls
