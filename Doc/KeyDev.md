# KeyDev
The editor mostly stays in a `GetKey()`/`PutKey()` loop. The putkey portion is where keys are acted-upon. TempleOS has a chain of putkey hndlrs in a Circular Queue[^1] with priorities. The highest priority hndlrs can choose to terminate handling, otherwise, the keys get sent on down the chain.

`KeyDevAdd()` defines a putkey device with a priority. "Device" might be a misnomer. Currently, the following are defined:

```
Priority    Hndlr
---------- ---------
0x20000000 MyPutKey()            user handler
0x40000000 KDInputFilterPutKey() for In(), InStr(), and InFile() handling.
0x60000000 KDRawPutKey()         nonwindowed direct to video mem debug output. 
0x80000000 KDDocPutKey()         standard document cmds
```
Since handling individual keys is slow, TempleOS supports `PutS()` as well. If no puts hndlr is defined, individual keys are sent.

`CDoc.user_put_key`[^2] and `CDoc.user_put_s`[^2] are call back routines which offer some neat tricks. See [JukeBox.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/JukeBox.HC). There is a var `CDoc.user_put_data`[^2] which gets passed to them.

[^1]: See HI:Data Types/Circular Queue

[^2]: See MN:CDoc
