# Memory Overview

Paging is practically not used. 64-bit mode requires paging, however, so it is identity-mapped -- virtual identical to physical. All tasks on all cores use the same page table map, just as though all addresses are physical addresses. 2Meg or 1Gig page table entries are used. Nothing swaps to disk.

In TempleOS, the lowest 2Gig of memory is called the code heap. TempleOS's compiler always uses 32-bit signed relative JMP & CALL insts because 64-bit CALLs take two insts. With signed +/- 32-bit values, code can only call a function within 2Gig distance. Therefore, TempleOS keeps all code in the lowest 2Gig memory addresses including what would normally be called "the kernel". Two Gig is plenty for code, don't worry.

You can create new, independent heaps using `HeapCtrlInit()`. Then, use the `CHeapCtrl` as the 2nd arg to `MAlloc()`. See `HeapLog()` for an example.

Memory alloced by a task will be freed when the task is killed. The [Adam Task](./Glossary.md) is a task that never dies. His memory is like kernel memory in other operating systems. See `ACAlloc()`, `AMAlloc()`, `AMAllocIdent()` and `AStrNew()`.

All of the regular page tables are marked, "cached". When accessing hardware, however, you need uncached page table. The lowest 4Gig addresses have an alias to access hardware located toward the top of mapped space, 0x01AA000000. See [`dev.uncached_alias`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KMain.HC).

During an extended powered-on session of TempleOS, in theory, memory will become fragmented, requiring a reboot. It has never happens to me.

See `MemRep()` and [MemDemo.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/MemDemo.HC).

## Single System-wide Mem Map

  - `0x0000007C00 - 0x0000036AEF` - Kernel module, placed here by the boot-loader, `BOOT_RAM_BASE`[^1].

  - `0x0000096600 - 0x0000096FFF` - Boot block relocated here before loading the Kernel module, [BootDVD](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootDVD.HC) & [BootHD](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Boot/BootHD.HC).
  - `0x0000097000 - 0x0000097030` - Multicore start-up vect code, `MPN_VECT`[^2].
  - `0x000009F000 - 0x000009FFFF` - Extended BIOS data area.
  - `0x00000A0000 - 0x00000BFFFF` - VGA graphics mem with alias at `text.vga_alias`.
  - `0x0000100000 - 0x0000101FFF` - `CSysFixedArea`[^3] for misc.
  - `0x000010F000 - 0x007FFFFFFF` - Code Heap mem.
  - `0x00E0000000 - 0x00FFFFFFFF` - 32-bit devices could alloc memory at 0xF0000000 going up, but this is wrong, since some PCs already have devices at 0xF0000000. No PCI devices are supported, so `Mem32DevAlloc()` flaws are not an issue.
  - `0x0080000000 - ~0x00DFFFFFFF + 0x0100000000 - ~0x01A9FFFFFF` - Data Heap mem. (The physical memory that exists in this range is data heap.)
  - `0x01AA000000 - 0x02A9FFFFFF` - Uncached alias of first 4Gig. (For 32-bit device access.)
  - `0x02A9FFFFFF` - 64-bit devices are alloced with `Mem64DevAlloc()` counting bwd, but no PCI devices are actually supported.

Note: There is a break in the data-heap block pool. This has no effect except the obvious effect that fragmentation has on contiguous requests. I can `MAlloc()` an 8Gig chunk on my 12Gig machine. I can `MAlloc()` an 32Gig chunk on my 64Gig machine. 

Note: For systems with less than 2Gig RAM, the code and data heap block pools are the same. For systems with 2-4Gig of RAM, the code heap is 1/4 of the total. See `BlkPoolsInit()`.

## History

In 2003, I wanted to make a no-paging ring-0-only 64-bit operating system for super speed with simplicity and full access. With paging, every memory request requires 5 accesses -- it must access the address itself, 4K, 2Meg, 1Gig, and 512Gig page tables, but the CPU's translation look-aside buffer mostly removes the penalty for using paging. So, I did not want to use paging, but long mode requires it. I did the next best thing -- I identity-mapped everything and achieved the simplicity I was after with subtle performance boosts, not wasting time changing address maps. And, I look forward to the day I command Intel to make an optimized no-paging long mode.

I needed VGA `0xA0000 - 0xBFFFF` memory to be write-through and `0xE0000000 - 0xFFFFFFFF` to be uncached for various devices. All 64-bit computers allow stopping address translation at 2Meg page size, not using 4K. I wanted to use 2Meg for everything because it's faster, with one less level of page tables. I had to make `0xA0000 - 0xBFFFF` write-through, though, so I could not use 2Meg size on the lowest page. I did the lowest 2Meg area as 4K pages. I also unmapped the first 4K to cause a fault when dereferencing NULL.

In 2016, I came-up with an alternate idea. I double mapped the lowest memory with an alias that was uncached. Accessing the lowest 2Meg area directly was cached but the alias I created up at the top of address space was uncached. See `UncachedAliasAlloc()`. Unfortunately, I could no longer boast of the simplicity of identity mapping everything. Since many of my users are familiar with `0xA0000 - 0xBFFFF`, it is actually pretty seriously unfortunate that they cannot use the easy-to-understand numbers of `0xA0000 - 0xBFFFF`, but must access the relocated alias location. See [`text.vga_alias`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KMain.HC). I also no longer cause a fault when dereferencing `NULL`.

Then, I switched to 1Gig page sizes. For the lowest 4Gig, I set-up an alias up at the top of address space. See `UncachedAliasAlloc()`. Not all computers support 1Gig page tables, however, so I also support 2Meg.

My original plan was to allow changing the page tables as needed, so I had code for taking control of 2Meg pages and marking them uncached or whatever. When I did a HDAudio driver, I requested some 32-bit address space as uncached. Today, all of the first 4Gig can be accessed without caching at the [`dev.uncached_alias`](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KMain.HC).

[^1]: See MN:BOOT_RAM_BASE

[^2]: See MN:MPN_VECT

[^3]: See MN:CSysFixedArea
