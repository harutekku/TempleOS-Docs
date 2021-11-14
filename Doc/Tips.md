# Tips

Turn-off or reboot (`<CTRL-ALT-DEL>`) at any time, except during disk writes. Writes are not cached. 

Use `Seed()` and the cmd line to switch `Rand()` to non-timer mode and replay games you like.

64-bit values are most efficient for the compiler.

See Key Map for a list of defined keys. Define your own keys in `MyPutKey()`. See Keyboard Devices[^1].

`<ALT-m>` maximizes a window. `<ALT-SHIFT-w>` closes AutoComplete. `<ALT-w>` brings back AutoComplete. `<ALT-v>` vertically tiles windows. `<ALT-h>` horizontally tiles windows. The ALT keys are defined in `~/HomeKeyPlugIns.HC`. You can customize them.

If you make changes to TempleOS files in your `/Home` directory, generally you reboot to make them take effect. (You don't compile anything.) You should have two TempleOS partitions on your hard drive because a syntax error in a start-up file will make the partition unbootable. Boot to the second partition or boot to a standard TempleOS CD/DVD and use `Mount()` to mount your hard drive.

I copy my files to a mirrored ident partition, periodically with `CopyTree()` commands in scripts. I do merge commands with a menu entry like this:
```holyc
Merge("C:/*", "D:/*", "+r+d"); to check my changes.
```

`<CTRL-m>` at the cmd line to access your PersonalMenu. Place macros there with `<CTRL-l>`, or icon-like sprites with `<CTRL-r>`. Use the Pop-Up option on macros to `Spawn()` a task to run a file. It dies when it is finished. This returns mem to the system. Be sure to press `<CTRL-s>` to save your macro/menu area after making changes.

You can use ans in cmd line expressions. It holds the res the last cmd line operation. You can use the cmd prompt as a calculator by just entering expressions like `1 + 2 * 3;`. F64 ress can be accessed with ansf.

Use the PullDown menu at the top of the scrn to learn commands, or for finding the keyboard controls to games.

You can adjust the mouse movement rate by setting global vars in your start-up file. See mouse scale[^2].

You can set your local time zone by setting the `local_time_offset`[^3] global var in a start-up file. It's units are `CDATE_FREQ`[^4]. See local time[^2].

`<CTRL-SHIFT-L>` in the editor to reindent a [HolyC](./HolyC.md) function or renumber an asm routine's local labels.

You can use filter_lines in the editor text search form (`<CTRL-f>`) to temporarily display just lines near each match. A value of filter lines set to 5 will display lines within 5 lines of matches. Then, you can do another find to a different string and achieve a AND search. When finished, press `<ESC>`.

You can recompile and reinstall the kernel with `BootHDIns()`. You'll probably want to make a function for recompiling that uses the `In()` function to answer the cfg questions. See my technique [Cfg Strs](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSCfg.HC), [Update Funs](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSDistro.HC).

`Scale2Mem(min, max, limit = 2 * 1024 * 1024 * 1024)` can be used for cfg questions when recompiling. The `BootHDIns()` cfg prompts accept expressions, not just numbers. The dft disk cache is `Scale2Mem(0x80000, 0x8000000)`.

You can permanently disable AutoComplete commenting-out `ACInit()` in `~/HomeSys.HC`.

Boolean expressions not in if stmts don't have short circuit logic and are compiled inefficiently.

You can use `progress1 - progress4` in your programs for whatever you like. They're just global vars that are shown on the wallpaper. The original intent was to indicate how far along operations were. There's no coordination, so different apps might interfere. I use them most for debugging--just values easily viewed. See [Progres.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Progress.HC).

Use `DocMax()` to adjust the size of the cmd line buf. It counts `CDoc`[^5] entries, not lines.

Many data structures have a user_data member. Those are available for you to store a data item, for convenience. `CTask`[^6], `CDocEntry`[^7] and `CDirEntry`[^8] have them. You shouldn't encounter conflicts with TempleOS using them.

If, for some strange reason, you wanted to reduce mem usage, make a smaller disk cache when you recompile the kernel; disabling AutoComplete; Specify smaller stk sizes when doing `Spawn()`, chang `MEM_DFT_STK`[^9], and using `DocMax()` to reduce the cmd line buffer size.

Filenames ending in ".Z" will be automatically compressed and uncompressed when read or written. The compression method is not supported by other operating systems. You can store files uncompressed by `Move()`ing them to a filename not ending in ".Z". See [TOSZ](./TOSZ.md) if you want to uncompress while in Linux.

`Merge()` can be used to see what's changed. The `+d` flag will show differences of files which have changed and allow you to merge code. (The `+r` flag will recurse.)

There is a utility `LinkChk()` which will check for broken links in documentation.

You can use `Option(OPTf_WARN_PAREN, ON)` to find unnecessary parentheses in code.

You can use `Option(OPTf_WARN_DUP_TYPES, ON)` to find unnecessary local var type stmts.

`Option(OPTf_ECHO, ON)` can be placed in [StartOS.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC) to echo start-up scripts.

Use `Plain()` to edit a plain text file. You'll need this if your file has $'s. Use the `ToDolDoc()` utility to convert plain text to DolDoc's by doubling $'s.

Use `Silent()` to disable scrn text output.

Grab-scroll any window at any time with `CTRL-LEFT-MOUSE-DRAG`. Null grab-scrolling with `CTRL-RIGHT-MOUSE`.

Use `<CTRL-ALT-z>` to zoom-in and `<CTRL-ALT-SHIFT-Z>` to zoom-out. You can scroll by moving to the edge of the window. Set `gr.continuous_scroll`[^10] to TRUE if you want. 

Use `<CTRL-ALT-g>` and `<CTRL-ALT-SHIFT-G>` to display a grid on the scrn.

Use `<CTRL-ALT-a>` to enter an extended ASCII char.

Use `<CTRL-ALT-f>` to toggle between [Std Font](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/FontStd.HC) and [Cyrillic Font](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/FontCyrillic.HC).

Use `<CTRL-ALT-s>` will capture the scrn as a sprite on the clip. You can save the cmd line doc as text with `<CTRL-a>`.

You can save a sprite as a .GR file in `<CTRL-r>` on the Sprite BitMap Menu.

You can eye-dropper colors in the `<CTRL-r>` sprite editor by pressing `c`. Press `t` for transparent.

There are handy functions -- `F()`, `R()`, `FD()` and `RD()` which are defined in `~/HomeWrappers.HC`. You are encouraged to change them and add more. They will perform find-and-replace operations accross multiple files. The `+l` flag is particularly useful since it limits to whole labels. The `+lb` and `+la` flags limit to whole labels just before or after. You are encouraged to add or modify handy wrapper functions to make cmd line operations easier.

When using `Find()` while modifying code, work from the bottom-up so that line numbers are correct. If you work top-down, then inserting or deleting lines causes the lower file links will be incorrect.

You can save files after making changes, anytime you are within the editor, like when viewing help/macro files. `<CTRL-a>` saves as, `<CTRL-s>` saves with the same name in the scrolling title bar. Hitting `<ESC>` will exit and save. (`<SHIFT-ESC>` will abort). You can save the cmd line window to a file, too, since you're actually in the editor when you're at the cmd line.

When using `<CTRL-l>` to insert links in documents, you can usually leave the Tag Text blank and it will be filled-in automatically based on other entries.

There is a feature of the precompiler that allows code to be executed in the middle of compilation and data inserted into the compilation stream.

If you output to the cmd line and wish to allow users to scroll around and view data, you can use `View()`.

Use `View()` in Pop-up macros to linger until the user presses `<ESC>` or `<SHIFT-ESC>`.

You can access the word under the cursor at `ac.cur_word`[^11].

You can reactivate AutoComplete after closing it by pressing `<CTRL-Fun Key>` or `<ALT-w>` if you have it defined.

`<CTRL-SHIFT-T>` to toggle to/from plain text just the `CDoc`[^5] cmd under the cursor. See [TextDemo.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/DolDoc/TextDemo.HC).

If you toggle to plain text when you are working with graphics in a document, you can add duplicate entries for sprites by entering a `$SP...$` cmd with the same num.

If you toggle to plain text when working with graphics, you can add a str to the `$SP...$` entry to keep track of it. Try `$SP,"`<2>`",BI=2$` where '2' is the sprite num.

I use spaces-to-tab operations on all my src files to keep them small. You have to be careful, though, because spaces in strings will be converted. I use `<SHIFT-SPACE>` ' ' in such cases. See `S2T()` for spaces-to-tabs.

You can edit an existing sprite by putting the cursor on it and pressing `<CTRL-r>`.

When editing a sprite, you can cut and paste the elements in the sidebar text list window.

I recommend keeping CSprite in vect format until you are done creating them, so you can edit the ctrl points. Then, convert them to bitmaps, so the flood fills work well. If you are doing interpolation, however, they must be vect.

`GrFloodFill()` is slow. `GrRect()` is fast.

You can customize the wallpaper. See [WallPaperFish.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/WallPaperFish.HC).

Your RAM disks will not be reformated when you reboot if the memory location has not changed and it finds the disk intacted.

`try { } catch { }` in a function will cause all vars to be non-reg.

Using a sub-int array, `i.u8[3]`, for example, will force a local var to non-reg.

You can delete the `~/Registry.HC.Z` file. The policy is that deleting it will restore defaults. It is a text doc, if you want to edit it. Be careful of tree indentations.

Study [MemRep.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Utils/MemRep.HC) and `WallPaper()` to learn how the system resources are put together.

The editor's sel-text mechanism allows for disjoint portions of sel text. This is a feature, not a bug -- you can cut-and-paste disjoint text.

`cnts.time_stamp_freq`[^12] is continuously calibrated. Be careful because expressions might decrease. Take a snap-shot, like this: `timeout = GetTSC + cnts.time_stamp_freq * seconds;` and compare against `GetTSC()`. I recommend just using `tS`[^13] or `cnts.jiffies`[^12].

Use `HeapLog()`, `HeapLogAddrRep()` and `HeapLogSizeRep()` to find leaks. Don't be confused by `CDoc`[^5] allocations. Those are generated when text is written to the cmd line buffer.

For advanced heap debugging, play with `_CFG_HEAP_DBG`[^14]. You're on your own.

You can use `Type()` to display .GR files.

Use `Man()` to jump to short sym name src code.

Use `Fix()` to edit and fix the last compiler err.

You can use `<CTRL-SHIFT-L>` to do a check for compile errors.

You can use `DocOpt()` to optimize links. (Mostly just removes .Z)

`ZipRep"$()` can highlight src files with lots of redundancy.

With start/end, common trailing code is fast. Common leading code is slow.

The first line of the [Psalmody](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/) [HolyC](./HolyC.md) song files is a comment with a category recognized by [`JukeBox()`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/JukeBox.HC). The categories are "no nothing", "has words", "has graphics", or "special". The third character in the song comment is a digit rating number, shown in [`JukeBox()`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/JukeBox.HC). You can set the song rating in [`JukeBox()`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/JukeBox.HC) by pressing 0-9. You can press `<DEL>` to delete songs.

## Credits
  - _Linux_ is a trademark owned by Linus Torvalds.

[^1]: See HI:Keyboard Devices/System

[^2]: See FF:~/HomeLocalize.HC

[^3]: See MN:local_time_offset

[^4]: See MN:CDATE_FREQ

[^5]: See MN:CDoc

[^6]: See MN:CTask

[^7]: See MN:CDocEntry

[^8]: See MN:CDirEntry

[^9]: See MN:MEM_DFT_STK

[^10]: See MN:CGrGlbls

[^11]: See MN:CAutoCompleteGlbls

[^12]: See MN:CCntsGlbls

[^13]: See MN:tS

[^14]: See MN:\_CFG_HEAP_DBG
