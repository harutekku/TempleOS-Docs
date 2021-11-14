# Hash
There is a symbol (hash) table for each task. When a sym is not found, the parent task's sym table is checked. All tasks chain back to the `Adam` task.

TempleOS sym tables are implemented with an array of linked-lists. A num is generated from a string by `HashStr()` to index into the array of linked-lists. Multiple strings can generate the same num, so linked-lists are built. Newer entries overshadow older ones.

There are various types of entries. See Hash Entry Types[^1].

Symbol Look-up (Used many places including the [JIT Compiler](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Compiler/Lex.HC) and [Loader](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KLoad.HC).):
1. Symbol name is hashed[^1] by adding and shifting the ASCII of all chars.
2. hash table `CHashTable->body[]` array is indexed.
3. Linked-lst is traversed until match of text and type of entry.
4. If not found, hash table `CHashTable->next` table is searched.

Duplicate entries are allowed -- they overshadow old entries.

Address-to-Symbol Look-up (Slow because not important. We could use trees.):
1. FunSeg Cache is scanned[^2].
2. Hash Tables are scanned[^3].

[^1]: See MN:SYS_HASH_STR

[^2]: See MN:FunSegCacheFind

[^3]: See MN:FunSegFind
