# File Manager

## Controls:
  - `<SHIFT CURSOR>` - Select files.
  - `<CTRL-y>` | `<DEL>` - Delete file or tree.
  - `<CTRL-c>` | `<CTRL-INS>` - Copy select files to clip.
  - `<CTRL-v>` | `<SHIFT-INS>` - Paste clip.
  - `LEFT-CLICK->drag-drop` - Move a file or tree to a dir.
  - `LEFT-CLICK` | `<SPACE>` - Edit file.
  -`<SHIFT-SPACE>` - Edit Plain Text File.
  - `RIGHT-CLICK` | `<ENTER>` - Bring-up menu.
  - `<F5>` - `#include` file.
  - `<SHIFT-F5>` - `Adam` `#include` file.
  - `r` - Rename file.
  - `d` - Make Dir.
  - `c` - DskChg (Remount removable media).  Do not do this on blank disks.
  - `f` - Format drive.
  - `i` - Mount ISO.C file.
  - `u` - Unmount drive(s).
  - `m` - Make CD/DVD ISO.C file. This creates a [RedSea](./RedSea.md) ISO file image of the dir the cursor is on. The name of the ISO file is `/Tmp/CDDVD.ISO.C`[^1] `blkdev.dft_iso_c_filename`[^2] and can be redefined in your start-up scripts. You may wish to place it on a different drive.
  - `B` - Burn CD/DVD ISO file. This burns a CD/DVD using the image file, `/Tmp/CDDVD.ISO`[^1] `blkdev.dft_iso_filename`[^2] to the drive the cursor is on.

## Instructions on Using CD/DVD's
If you have not recompiled Kernel and defined your CD/DVD drive, exit the FileMgr and use `Mount` to define your CD/DVD drive. Place a CD/DVD in the drive and press `c` when on top of the CD/DVD drive letter to mount the drive. It will call `DskChg()`, the TempleOS cmd to mount removable media.

## Instructions on Burning CD/DVD's
Create a temporary dir to hold files and copy files into the holding dir. Make an ISO image of the dir by pressing `M` when on top of the dir. Press `B` when on top of the CD/DVD ROM drive to burn the ISO, `/Tmp/CDDVD.ISO`[^1] `blkdev.dft_iso_filename`[^2], to disk. If you have not recompiled Kernel and defined your CD/DVD drive, exit the FileMgr and use `Mount`.
See [Making Your Own Distro](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/DoDistro.HC)

[^1]: See D:DFT_ISO_C_FILENAME

[^2]: See MN:CblkDevGlbls
