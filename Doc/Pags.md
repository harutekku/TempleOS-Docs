# Pags
The word _Pag_ refers to an arbitrilly created `MEM_PAG_SIZE`[^1] unit of heap allocation. TempleOS does not alter the CPU page tables after setting them up at boot in `SYS_INIT_PAGE_TABLES`[^2], so the CPU hardware page size is rarely important.

[^1]: See MN:MEM_PAG_SIZE

[^2]: See MN:SYS_INIT_PAGE_TABLES
