# RedSea File System

The RedSea file system is a simple, 64-bit, file system which is similar to FAT32, but with absolute block addresses instead of clus, fixed-sized 64-byte directory entries and no FAT table, just an allocation bitmap. A clus is just one 512 byte sector. Files are stored in contiguous blocks and cannot grow in size.

```holyc
#define CDIR_FILENAME_LEN 38    // Must include terminator zero
```
The following bit field shows valid 8-Bit ASCII filename characters.

```holyc
U32 char_bmp_filename[8] = { 0x0000000,  0x03FF73FB, 
                             0xEFFFFFFF, 0x2FFFFFFF, 
                             0xFFFFFFFF, 0xFFFFFFFF,
                             0xFFFFFFFF, 0xFFFFFFFF
                           };

public class CDirEntry {         // 64-byte fixed size
  U16 attr;                      // See MN:RS_ATTR_DIR. I would like to change these.
  U8 name[CDIR_FILENAME_LEN];    // See MN:char_bmp_filename, MN:FileNameChk
  I64 clus;                      // blk - One sector per clus.
  I64 size;                      // In bytes
  CDate datetime;                // See  DateTime, Implementation of DateTime /Kernel/KDate.HC
};

public class CRedSeaBoot {       //RedSea is type FAT32 in partition table to fool BIOS.
  U8 jump_and_nop[3];
  U8 signature, reserved[4];     // MBR_PT_REDSEA=0x88. Distinguish from real FAT32.
  I64 drv_offset;                // For CD/DVD image copy.
  I64 sects;
  I64 root_clus;                 // root_blk
  I64 bitmap_sects;
  I64 unique_id;
  U8 code[462];
  U16 signature2;                // 0xAA55
};
```
See [FileSysRedSea.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/BlkDev/FileSysRedSea.HC) and [DskISORedSea.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/DskISORedSea.HC).

Files with names ending in .Z are compressed. See [Compress.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Compress.HC).

To replace ISO9660, make hard-drive partition image of a measured size and copy onto a CD/DVD starting at about sector 20, with EL TORITO booting. 512-byte sectors will be placed on top of 2048-byte CD/DCD sectors, so there will be four blocks per CD/DVD sector.

RedSea file system has no bad block table and no redundant allocation table.

See [Block Chain](./BlkChain.md) for RedSea allocation bitmap discussion.

[Reliability](./Reliability.md) for RedSea reliability discussion.
