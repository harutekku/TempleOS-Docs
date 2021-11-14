# Profiler
The profiler records where the CPU was executing when the 1000Hz timer interrupt occured, so you can learn where time is spent.

Use the `Prof()` depth argument to record a hit in the N routines which called the current routine, as well.

When done collecting statistics, use `ProfRep()` for a report. You might need a `DocMax()` to expand the command line window buffer to fit it all.

Study the code. The profiler is very simple. You might want to enhance it or modify it to debug something in particular.
