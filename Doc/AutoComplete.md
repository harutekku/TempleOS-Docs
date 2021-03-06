# AutoComplete
AutoComplete is the window on the right of the scrn. `ACInit()` collects words from all text files in subdirectories. Normally, the call to `ACInit()` is in [HomeSys.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/HomeSys.HC). It provides auto-complete for typing, jump-to-code and jump-to-dictionary functionality.

## Comamnds
- `<ALT-SHIFT-A>`	Closes the AutoComplete window.
- `<ALT-a>`	    	Opens the AutoComplete window.
- `<CTRL-SHIFT-F1>`	Jumps to the source code for 1st symbol in the window.
- `<CTRL-SHIFT-F2>`	Jumps to the source code for 2nd symbol in the window.
- `<CTRL-SHIFT-Fn>`	Jumps to the source code for n-th symbol in the window.
- `<CTRL-SHIFT-1>`	Jumps to the dictionary for 1st symbol in the window.
- `<CTRL-SHIFT-2>`	Jumps to the dictionary for 2nd symbol in the window.
- `<CTRL-SHIFT-n>`	Jumps to the dictionary for n-th symbol in the window.
- `<CTRL-F1>`	Autocompletes the 1st symbol in the window.
- `<CTRL-F2>`	Autocompletes the 2nd symbol in the window.
- `<CTRL-Fn>`	Autocompletes the n-th symbol in the window.
- `<CTRL-1>`	Autocompletes the 1st dictionary word in the window.
- `<CTRL-2>`	Autocompletes the 2nd dictionary word in the window.
- `<CTRL-n>`	Autocompletes the n-th dictionary word in the window.

If you have the raw Project Gutenberg dictionary file, you can generate the TempleOS processed dictionary files with the stand-alone program [ACDictGen](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/AutoComplete/ACDictGen.HC)