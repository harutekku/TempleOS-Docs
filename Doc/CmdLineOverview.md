# Command Line Overview

The cmd line feeds into the [HolyC](./HolyC.md) compiler line-by-line as you type. A stmt outside a function executes immediately. Remember to add a semicolon.

Look-up the function headers with AutoComplete by hitting `<CTRL-SHIFT-F1>` after typing the first few letters.

Click here[^1] to see the directory cmd header. It accepts default args from C++.

```holyc
Dir("*.DD.Z");
Dir;                // If you don't have args, you don't need parenthesis.
```

Directories are referenced with `/` not '\\'. There is a current directory, but not a path. To run a program, you typically `#include` it. There are several shortcuts for `#include`ing files. Right-click or hit `<ENTER>` on a directory listing or press `<F5>` while editing.

```holyc
Ed("NewFile.HC.Z"); // Invokes the editor. See Doc Link Type (LK_FILE).
```

Most filenames end in `.Z` because they are stored compressed.

Drives are specified with a letter. The boot drive is specified with a `:`. The home dir drive is specified with a `~`.

```holyc
Drv('B');           // B drive
```

The drive can be specified in a `Cd()` command as in:

```holyc
Cd("B:/Tmp");       // B drive
Cd("::/Demo");      // Boot drive
```

The home directory is specified with a `~`.

```holyc
Cd("~/Psalmody");   // See /Home dir in ./GuideLines.md.
```

If a file is not found, `.Z` is added or removed and a search is done, again. If a file is still not found, all parent directories are searched.

You can place macros in your [PersonalMenu.DD](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/PersonalMenu.DD) for `Cd()` commands. `<CTRL-m>` to access your menu.

```holyc
Find("needle", "/Demo/*.HC.Z;*.DD.Z;")  // See File Utils in ./FileUtils.md.
```

Cmd Line Routines[^3]

[^1]: See MN:Dir

[^2]: See HI:Cmd Line (Typically)

