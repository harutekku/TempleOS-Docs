# Style guide for rewritting DolDocs to Markup
  - The following objects should be enclosed in ``
    - Directory paths, i.e `~/Example.HC`
    - HolyC functions, i.e `Spawn()`
    - Keyboard shortcuts, i.e `<CTRL-l>`
    - File names, i.e `DoOnce.HC`
    - File extensions, i.e `.HC`
    - Internal TempleOS programs, i.e `Adam`
    - Function argument values, i.e `"+r"`
  - All HolyC code should be enclosed in triple `
    - Exception being single-line statements in the middle of another statement
  - Try to link as much resources as possible
    - When referencing other resource, don't include file extension if not necessary
    - If it's impossible to locate the source with certain name/function, write its name in a footnote[^1]
  - All third-party software mentionned in the `## Credits` section should be in _italic_

[^1]: i.e: See MN:CblkDevGlbls
