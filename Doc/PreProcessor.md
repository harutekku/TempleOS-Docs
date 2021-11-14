# PreProcessor

There is no separate preprocessor pass. The parser front-end calls `Lex()` which has the preprocessor built-in. The compiler looks ahead a token, most of the time, so you might throw an extra semicolon after a directive if it's not taking affect right away.

Put an extra semicolon `#exe {Cd("DirName");;}` in case a `#include` follows.

## List of directives
```holyc
#include ""     // There is no angle bracket <> form of this directive.
#exe {}         // Will execute code at compile-time and can be used to insert code into the stream being compiled using StreamPrint()
#define         // Define string const
#assert         // Print a warning during compilation if an expression is not true. 
#if             // Include code if an expresion is true.
#else
#endif
#ifdef          // Include code if a sym is defined.
#ifndef               
#ifaot          // Include code if in AOT compiler mode.
#ifjit    
defined();      // Is a function that can be used in expressions.
#help_index
#help_file      // See ./HelpSystem.md
```

See [PreProcessor](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Compiler/Lex.HC).
