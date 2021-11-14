# Time and Date
TempleOS uses a 64-bit value, `CDate`[^1], for date/time. The upper 32-bits are the days since Christ. The lower 32-bits store time of day divided by 4 billion which works out to 49710ths of a second. You can subtract two `CDate`[^1]'s to get a time span.

Use `CDATE_FREQ`[^2] to convert.

[^1]: See MN:CDate

[^2]: See MN:CDATE_FREQ
