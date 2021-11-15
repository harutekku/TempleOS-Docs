# Streams
There are no streams in the traditional sense. The cmd line output gets sent to the cursor location of a document being edited and by using cursor keys, text can be injected all over the document. Sprites[^1] can be injected and are not serialized! Furthermore, the input can come from triggering macro widgets. See [Doc Overview](./DolDocOverview.md) and Doc Routines[^2].

If you had a remote term and sent key Scan Codes[^3], the user would press `<CTRL-m>` to access his Personal Menu to trigger his macros. However, the local [PersonalMenu.DD](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/PersonalMenu.DD) might differ from the remote, causing loss of sync between local and remote sessions. Also, the window size of local and remote might differ, so word-wrapped text would be different. Injecting output text with different windows sizes would cause remote and local documents to not be in sync.

See [Char Overview](./CharOverview.md) and Char Routines[^4].

You can send characters into StdIn. See `In()`, `XTalk()` and InFile[^5].

[^1]: See HI:Sprites

[^2]: See HI:DolDoc

[^3]: See MN:SC_INS

[^4]: See HI:Char

[^5]: See HI:InFile
