# Once

```
KMain()
  includes "/StartOS.HC"
    includes "~/MakeHome.HC"
      includes "~/HomeSys.HC"
        calls StartUpTasks()
          includes "~/Once.HC"
            calls OnceExe()
```
`AOnce()` appends src code to `~/Registry.HC` Once/Adam tree, executed at next boot by `Adam`.

`Once()` appends src code to `~/Registry.HC` Once/User tree , executed at next boot by first User term.

At boot, `OnceExe()`, executes Once/Adam tree, `AOnceFlush()`s it, executes Once/User tree and `OnceFlush()`s.
