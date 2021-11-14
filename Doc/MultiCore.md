# Multicore
TempleOS does master-slave multicore instead of SMP. Core0 is the master. The master core's applications explicitly assign computational jobs to other cores and the TempleOS scheduler does not move tasks between cores.

There are multicore safe locks for file access and heap allocations, however, so TempleOS is symmetrical in some sense. See [LoadTest.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/MultiCore/LoadTest.HC).

Only tasks on Core0 can have windows, but other cores can help render them.

Each core has an executive [Seth Task](./Glossary.md) which is the father of all tasks on that core. [Adam](./Glossary.md) is the [Seth Task](./Glossary.md) on Core0.

You give a job to a [Seth Task](./Glossary.md) with `JobQue()` and get the result with `JobResGet()`. You spawn a task on any core with `Spawn()`.

Note: You must use the `LOCK` asm prefix when changing shared structures in a multicore environment. The `LBts()`, `LBtr()` and `LBtc()` insts have `LOCK` prefixes. The compiler has a `lock{ }` feature but it doesn't work well. See [Lock.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/MultiCore/Lock.HC).

See [Transform.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Transform.HC).

See [MultiProc.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/MultiProc.HC).
