# Menus
A pull-down menu appears when you move the mouse to the top of the scrn. Menus are created with `MenuPush()`, `MenuFilePush()`, `MenuNew()` or `MenuFile()` and assigned to `Fs->cur_menu`. The format is:
```holyc
File {
  Open(,'O');
  Save(,'S');
  Exit(,CH_SHIFT_ESC);
}

Edit {
  Cut(,,SC_DELETE|SCF_SHIFT);
  Paste(,,SC_INS|SCF_SHIFT);
}
Misc {
  Opt1(MSG_CMD,M_OPTION1);
  Opt2(MSG_CMD,M_OPTION2);
}
Help {
  Help(,'?');
  About(,'/');
}
```
The first arg is the msg code and it is optional with the default being `MSG_KEY_DOWN_UP`[^1]. The second arg is the msg arg1 value which is ASCII[^2] of the key in the case of `MSG_KEY_DOWN`[^3]. The third arg is the msg arg2 value which is the [scan_code](./CharOverview.md) of the key in the case of `MSG_KEY_DOWN`[^3].

Press `<CTRL-SHIFT-l>` and "Insert ASCII/ScanCode".

See [PullDownMenu.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/PullDownMenu.HC).

[^1]: See MN:MSG_KEY_DOWN_UP

[^2]: See MN:CH_CTRLA

[^3]: See MN:MSG_KEY_DOWN
