# Compiler Options

## Using `Option()`
You might need to do
```holyc
#exe { Option(); }
```

## List of options
  - `OPTf_GLBLS_ON_DATA_HEAP`[^1] - without this option, global vars are placed in the code heap which is limited to 2Gig. In AOT modules, global vars take-up room in the `.BIN` file, so you might want to use this option, instead. You might wish to turn it on and off around specific vars. A disadvantage of data heap global vars in AOT modules is they can't be initialized.
  - `OPTf_EXTERNS_TO_IMPORTS`[^2] and `OPTf_KEEP_PRIVATE`[^3] -  are strange options, you'll never need. They're to allow the same header file for Kernel to act as `extern`s when compiling itself and `import`s when compiled by AOT modules.
  - `OPTf_WARN_UNUSED_VAR`[^4] - warning if unused var. It is applied to functions.
  - `OPTf_WARN_PAREN`[^5] - warning if parenthesis are not needed.
  - `OPTf_WARN_DUP_TYPES`[^6] - warning if dup local var type stmts.
  - `OPTf_WARN_HEADER_MISMATCH`[^7] - warning if fun header does not match.
  - `OPTf_NO_REG_VAR`[^8] - forces all function local vars to the stk not regs. Applied to functions.
  - `OPTf_NO_BUILTIN_CONST`[^9] - Disable 10-byte float consts for ã, log2_10, log10_2, loge_2. Applied to functions.

[^1]: See MN:OPTf_GLBLS_ON_DATA_HEAP

[^2]: See MN:OPTf_EXTERNS_TO_IMPORTS

[^3]: See MN:OPTf_KEEP_PRIVATE

[^4]: See MN:OPTf_WARN_UNUSED_VAR

[^5]: See MN:OPTf_WARN_PAREN

[^6]: See MN:OPTf_WARN_DUP_TYPES

[^7]: See MN:OPTf_WARN_HEADER_MISMATCH

[^8]: See MN:OPTf_NO_REG_VAR

[^9]: See MN:OPTf_NO_BUILTIN_CONST
