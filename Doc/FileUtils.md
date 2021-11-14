# File Utils

File util `FilesFind()` wildcard mask consists of a single base dir with multiple file masks separated by `;`. The `*` and `?` wildcard chars are accepted. The `~` is your home directory and `!` indicates an exclusion mask.
 
 ```
"/Kernel/*"             BaseDir: /Kernel    Mask: `*`
"/Demo/*.BMP*;*.GR*"    BaseDir: /Demo$FG$  Mask: `*.BMP*` | `*.GR*`
"/*.DD*;!*/Bible*"      BaseDir: /          Mask: `*.DD*` but not `*/Bible*`
```

See `FilesFindMatch()`.

Flags are either text or int values:
  - `FUF_RECURSE` - `+r` - Recurse
  - `FUF_SINGLE` - `+s` - Single File (Optimization for one file in mask.)
  - `FUF_FLATTEN_TREE` - `+f` - use with `+F`. Just use `+`, probably.
  - `FUF_JUST_DIRS` - `+D` - just directories
  - `FUF_JUST_FILES` - `+F` - just files (Flattens trees)
  - `FUF_CLUS_ORDER` - `+O` - sort by clus (move head one direction)
  - `FUF_JUST_TXT` - `+T` - just text files (`FILEMASK_TXT`)
  - `FUF_JUST_SRC` - `+S` - just src files (`FILEMASK_SRC`)
  - `FUF_JUST_AOT` - `+A` - just aot files (`FILEMASK_AOT`)
  - `FUF_JUST_JIT` - `+J` - just jit files (`FILEMASK_JIT`)
  - `FUF_JUST_GR` - `+G` - just graphic files (`FILEMASK_GR`)
  - `FUF_JUST_DD` - `+$` - just [DolDoc](./DolDocOverview.md) files (`FILEMASK_DD`)

See `ST_FILE_UTIL_FLAGS` when used in calling program taking text flags.
