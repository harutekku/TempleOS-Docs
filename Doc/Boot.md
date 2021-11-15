# Booting A PC
TempleOS only supports traditional BIOS booting, not the newer technique, UEFI. This document describes BIOS booting.

When you turn-on (power-up) a computer or you do a hardware reset, the computer starts executing the BIOS. Sometimes, you must change the BIOS boot order to boot the device you want.

The BIOS loads a boot sector from CD/DVD, hard disk or whatever. The boot sector runs in 16-bit real mode and often loads-in a second file that's bigger if it can't be done by just one sector. It's a safe bet that boot sectors are hand-coded assembly language. Most boot sectors use the BIOS to load-in the next stage.

Not only do boot sectors have a size limit, 512 bytes or 2048 bytes for CD/DVD, the files they load have to fit within 640K because they run in 16-bit mode. This means they usually can't just load the whole operating system and start it running. Some boot loaders, like Grub, have a capability of switching modes before handing-off control to the operating system. The operating system must load the rest of itself. With TempleOS, the [Kernel.BIN.C](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Kernel.PRJ) file is loaded by the boot sector. I try to put a minimum in the [Kernel Module](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Kernel.PRJ), so that it will always fit in 640K. When `Kernel.BIN` runs, it switches to 32-bit mode, then, to 64-bit mode allowing access to more memory. Then, it loads in the rest of TempleOS by executing [StartOS.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/StartOS.HC).

## Boot code
All the boot related code for TempleOS is in the [Boot](https://github.com/cia-foundation/TempleOS/tree/archive/Adam/Opt/Boot) directory

### CD/DVD boot sector
- [BootDVD.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootDVD.HC) - CD/DVD boot sector.
- [BootDVDIns.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootDVDIns.HC) - Prep for CD/DVD install by creating [0000Kernel.BIN.C](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/0000Boot/0000Kernel.BIN.C).
If you are curious about CD/DVDs, see [DskISORedSea.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/DskISORedSea.HC). To make a custom bootable CD/DVD, look [here](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/DoDistro.HC).

### Master boot loaders
- [BootMHD.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootMHD.HC) - Stage 1 Master HD boot loader.
- [BootMHD2.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootMHD2.HC) - Stage 2 Master HD boot loader.
- [BootMHDIns.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootMHDIns.HC) - Installs Master HD boot loader.
BootMHD goes on block zero. `BootMHD2.BIN.C` is stored as a file in a partition, risky and unusual, since most master boot loaders place stage 2 in a gap that's not in any partition. BootMHD2 displays a menu and boots a partition.

### Partition boot records
- [BootHD.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootHD.HC) - HD partition boot record.
- [BootHDIns.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootHDIns.HC) - Installs HD partition boot record.
BootHD is the boot record for a TempleOS partition. Each partition has its own partition boot record, the first block of the partition.

## Other info
My boot records don't access directories because that would make them too big for one block and would make them depend on a file system layout. Instead, they get patched with the LBA, logical block addresses, to load files. To update with a new TempleOS kernel, you must create a `Kernel.BIN.C`, `Kernel.PRJ` binary file and patch the boot loader so it knows the LBA blocks to load. Therefore, you usually recompile the kernel and update the boot sector at the same time with `BootHDIns()`, `BootMHDIns()` will install a master boot loader.

With TempleOS, `Kernel.BIN.C` and `Kernel.PRJ` loads `Compiler.BIN` and `Compiler.PRJ` so it can work with source code from then on. It compiles start-up scripts beginning with `StartOS.HC` into the [Adam Task](./Glossary.md)'s memory including the code in the `/Adam` and `/Home` directories.

It is possible to do a fast reboot without doing a hardware reset. You might do this when working on `Kernel.BIN.C` and `Kernel.PRJ` or your start-up scripts when you want to compile them effect. See `BootRAM()`.
