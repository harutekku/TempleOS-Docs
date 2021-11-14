# Time Cycles
Intel/AMD have an inst that returns the num of CPU cycles since boot. This is not a steady, calibrated real time value. TempleOS measures it and you can convert with `cnts.time_stamp_freq`[^1], a value continuously calibrated from other cnts.

[^1]: See MN:CCntsGlbls
