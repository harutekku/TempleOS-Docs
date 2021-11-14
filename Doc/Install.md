# Installing TempleOS
Burn a CD with software that supports ISO files. Then, boot it. It's a live CD, so you can look around with or without installing.

Dual booting with another operating system is the best way to use TempleOS. I only use it in a virtual machine because it won't boot natively on my machine, though. For native dual booting, you need a partition for TempleOS. Windows often comes with a restore disk that does not allow repartitioning. I recommend connecting a spare additional hard drive and using the BIOS to select which drive to boot.

The [OSInstall.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/OSInstall.DD) script will automate much of this. It runs if you boot the CD/DVD-ROM.

See [Boot](./Boot.md) for an overview of booting. See [Requirements](./Requirements.md) for supported hardware.

Two TempleOS partitions are highly recommended, so you can boot to a back-up and fix the primary when you work on it. Odds are, you only need a couple gigabytes for your TempleOS partitions.

## `Mount()`
Use if the drive is partitioned. This command mounts a drive making it accessible. For simplicity, sel 'C' as the first drive letter for your hard drive. The first partition will be 'C', second, 'D', etc. TempleOS needs 3 numbers to utilize a hard drive -- base0, base1, and unit. When you enter a hexadecimal number, do it like in C with a 0x prefix. If the probe was successful, you can just enter the number in the probe box instead of base0.

```holyc
DskPrt('C')  // use if drive is not partitioned
```
This will perform a special `Mount()` automatically.

WARNING: This command erases everything on a hard drive. It repartitions a whole drive and formats the partitions. This command should be skipped if you already have your hard drive partitioned.

WARNING: This command doesn't play well with other operating systems. You'll need to do a `BootMHDZero()` to restore your drive to a state where other operating systems can partition it.

## `Fmt('D', TRUE, FALSE, FSt_FAT32)`
This command formats a drive with FAT32 or the [RedSea](./RedSea.md) file system type. Use the drive letter of the partition in place of 'D'.

WARNING: If you are upgrading, be sure not to lose the file, `/0000Boot/OldMBR.BIN.C`.

## `CopyTree("T:/","D:/")`
This command is used to copy files onto a hard drive partition from the CD/DVD. Use the drive letter of the partition in place of 'D'.

## `BootHDIns('D')`
This command recompiles the source code on a drive and writes to the *drive's* boot record. You'll need to reenter the Mount[^1] information so it can be stored in the kernel.

## Use Linux's Grub or TempleOS - `BootMHDIns('D')`

The `BootMHDIns()` command places a boot loader on a drive. It saves the old master boot record to /0000Boot/OldMBR.BIN.C and replaces it. When you boot, you will have the option of booting the old master boot record. This command can be skipped if you already have a boot loader. Be sure not to lose the copy of the old boot record, like if you reformat the drive.

Delete `/0000Boot/OldMBR.BIN.C` if you want to get a fresh copy of a mbr, like if installing from your own custom CD containing it's own `/0000Boot/OldMBR.BIN.C` onto a system with a non-TempleOS boot loader.

If you have anti-virus software, it might object to having a different master boot record.


# Credits
  - _Windows_ is a trademark owned by MicroSoft Corp.
  - _Linux_ is a trademark owned by Linus Torvalds.

[^1]: See MN:Mount
