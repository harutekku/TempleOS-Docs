# Key Allocations

See Char[^1] for definition of scan codes.

See Key Map[^2] for a detailed list of key commands.

When you are at the cmd line, editing documents, browsing documentation and help, entering items in forms or in menu's, the DolDoc[^3] editor handles keys. It allows you to define your own key hndlrs in a `MyPutKey()` function. If you choose, you can catch keys, overriding the default hndlrs. See `DocPutKey()`. The following is an overview of key allocations.
  - `<ALT-keys>` & `<ALT-SHIFT-keys>` - Free for user configurations in your `MyPutKey()` hndlr, except for `ALT-BACKSPACE` (undo). There are a few examples pre-defined, but you can change them if you wish.
  - `<CTRL-ALT-keys>` & `<CTRL-ALT-SHIFT-keys>` - Handled at a system level, NOT by the `CDoc`[^3] editor. I reserve the right to alloc these, but in the mean time, you can define your own hndlrs with `CtrlAltCBSet()`. They operate either in a interrupt environment or in the window mgr when it queues kbd msgs. You can do `Raw()` output. `<CTRL-ALT-letter>` hndlrs take a scan_code as an arg.
  - `<CTRL-function key>` - Auto-completes local words.
  - `<CTRL-digit key>` - Auto-completes dictionary words.
  - `<CTRL-SHIFT-function key>` - Jumps to src code.
  - `<CTRL-SHIFT-digit key>` - Jumps to dictionary definition.
  - `<function keys> and <SHIFT-function keys>` - I reserve the right to alloc these, but there are some free now.
  - `<CTRL-key> and <CTRL-SHIFT-key>` - I reserve the right to alloc to these.  There are not many free `PutKeyHandling`
See Keyboard Devices[^4].

[^1]: See HI:Char

[^2]: See LM=KeyMap;View;

[^3]: See MN:CDoc

[^4]: See HI:Keyboard Devices/System
