# stdout Task
There is one `CDoc`[^1] for the task's border: `Fs->border_doc`. There is a pair for the task's client area: `Fs->put_doc` and `Fs->display_doc`. You can, optionally, do double buffering, otherwise `Fs->put_doc` is the same as `Fs->display_doc`. See [Spy.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Spy.HC).

[^1]: See MN:CDoc
