# Time Jiffy
One jiffy is one time slice. `cnts.jiffies`[^1] returns time slices since boot.

`SysTimerRead`[^2] reads the timer ticks since boot. It's not as fast as `GetTSC`[^3].

Use `JIFFY_FREQ`[^4] to convert `cnts.jiffies`[^1].

Use `SYS_TIMER_FREQ`[^5] to convert `SysTimerRead`[^2].

[^1]: See MN:CCntsGlbls

[^2]: See MN:SysTimerRead

[^3]: See MN:GetTSC

[^4]: See MN:JIFFY_FREQ

[^5]: See MN:SYS_TIMER_FREQ
