# Bit
These take a pointer to a bit field.
 - `Bt`	- Bit Test
 - `Bts` - Bit Test and Set to one
 - `Btr` -	Bit Test and Rst to zero
 - `Btc` - Bit Test and Compliment (toggle)
 - `BEqu` -	Set bit to value.

Bit operations are "atomic", no interrupt between the reading and writing the bit, important when multitasking. For multicore use "locked" forms.

These don't take a pointer, but the actual field.
- `Bsf` - Bit Scan Fwd (Pos of first low one bit or -1)
- `Bsr` - Bit Scan Rev (Pos of first high one bit or -1)
- `BCnt` - Bit Cnt (Cnt of set bits)
