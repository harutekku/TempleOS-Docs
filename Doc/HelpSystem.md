# `#help_index` 
The `#help_index` preprocessor compiler directive sets the topics for syms subsequently defined. You specify subtopics with a `/` tree hierarchy and separate multiple topics with a `;`. The index ctrls index[^1] links.

`public` causes a sym to appear in help_index reports.

## Syntax
```holyc
#help_file "filename[.DD.Z]"
```
The help file preprocessor directive makes a file into the heading of a index[^1] report for the current help index.

[^1]: See MN:LK_HELP_INDEX
