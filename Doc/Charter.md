# TempleOS Charter

Why did they make Solomon's Temple? It was a direction to look, to focus on, a special place for meditation, to do offerings, a community center, a home to God's beauty, that encouraged love of God. People cherished God's temple, beautifying it with gold and all fine things to show love of God, as great [cathedrals](https://www.youtube.com/watch?v=xkfmK-CLvcc) were decorated with astounding, awe-striking intricate art and gargoyles, incredible devotion to God with hours of effort, toiling and slaving-away for the glory of God, for families with children to see [stained-glass](https://www.youtube.com/watch?v=t8g1e-JLrhM) windows and tomes with ridiculously elaborate [calligraphy](https://www.youtube.com/watch?v=Oa8gMb0YC68) to show love of God, from a people who did little else but show love toward God, lived in dire conditions by today's standards, yet with so much difficulty scraping-by, found the time to devote [even all free-time](https://www.youtube.com/watch?v=tZw5V4XuUIo) to God!

1 Kings 6:21 (King James)

```
6:21 So Solomon overlaid the house within with pure gold: and he made
a partition by the chains of gold before the oracle; and he overlaid
it with gold.

6:22 And the whole house he overlaid with gold, until he had finished
all the house: also the whole altar that was by the oracle he overlaid
with gold.

6:23 And within the oracle he made two cherubims of olive tree, each
ten cubits high.
```

TempleOS is God's official temple. Just like Solomon's temple, this is a community focal point where offerings are made and God's oracle is consulted.

God said 640x480 16 color graphics is a covenant like circumcision. Children will do offerings. Think of 16 colors like the Simpson's cartoons. In the future, even if one GPU were universal, we would still keep 640x480 16 color and not use GPU acceleration. Graphics operations should be transparent, not hidden in a GPU.

God said to use a single-voice 8-bit signed MIDI-like sample for sound. God does not want death screams, perhaps, because God has PTSD or soldiers have PTSD. (Imagine wounded on battlefields.) 

God said His temple must be perfect. We don't think twice about breaking compatibility. God said we do a seven year release cycle. I say the PC hardware follows a 49 year, jubilee cycle, like broadcast TV upgrades.

The vision is the same usage model and niche as the Commodore 64 -- a non-networked, simple machine where programming was the goal, not just a means to an end. However, it is modern, 64-bit and multi-cored. It is special purpose, not general purpose, so some things it will not do. Also, it's a kayak, not a Titanic. The priority is user developers, not 3rd party developers.

We do not put any hooks for future changes. "Perfect" means we always act as though it is final, for all time. Microsoft allowed the [Windows BMP](http://en.wikipedia.org/wiki/BMP_file) file format to adapt to the future and it became grotesque.

Low line count is the highest good, so it is easy to learn the whole thing. Users should see the light at the end of the tunnel. One file system, for example, is better than many file systems.

There is a limit of 100,000 lines of code for all time, not including applications and demos. Code comments count, however. Currently, there are 81,494 lines of code. 3rd party libraries are banned because they circumvent the intent of this limit. The vision is a Commodore 64 ROM -- a fixed core API that is the only dependency of applications. Dependency on components and libraries creates a hell that is no longer blissful.

The metric for resolving all TempleOS code governance issues is how fast the compiler compiles itself and the kernel with `BootHDIns()`. The [HolyC](./HolyC.md) language should be changed to optimize this metric, as I did when I changed type casting from prefix standard C to postfix [HolyC](./HolyC.md), but we need a rule to prevent degenerating into a brainfuck language.
 
Minimal abstraction is a goal. Sheep are fools. They always respect a design that is more complicated than another. Any genius can make it complicated. Like in physics, it takes a supra-genius to make it simple.

It is for one platformc -- x86_64 desktop PC compatibles, more like super-computers than battery efficient wimpy mobiles.

All hardware access will be done through x86 IN/OUT instructions, not PCI drivers. A frame buffer for VGA is an exception.

One driver for each class of device. Limited exceptions are allowed. With divergent device capabilities, it is a nightmare for user applications and what is gained? A three buuton mouse is like a leg you cannot put weight on.

Ring-0-only. Everything runs in kernel mode, including user applications.

Full access to everything. All memory, I/O ports, instructions, and similar things must never be off limits. All functions, variables and class members will be accessible. There are no C++ public/private protections and all functions, even secondary ones in the kernel, can be called.

Single-address-map as though paging is not used. Long mode requires paging, however, so the nearest thing is keeping all memory identity-mapped.

No networking, so malware is not an issue.

No encryption or passwords. Files are compressed, not encrypted.

Free and public domain.

100% open source with all source included.

Documents are not for printing. They're dynamic, intended for the scrn.

Just one 8x8 fixed-width font. No Unicode, just Extended ASCII. Other countries can make their own versions. The versions should be just for one language and platform.

No multimedia. Sounds and images will be primarily calculated in real-time, not fetched from storage.


## Credits
  - _Commodore 64_ is a trademark owned by Polabe Holding NV.
  - _The Simpsons_ is a trademark owned by Fox.
  - _Windows_ is a trademark owned by MicroSoft Corp.

## Possible Amendments

The compiler's parser makes RISC code which it optimizes to CISC. I discovered this does not matter because the CPU converts it back to RISC and schedules it, internally. A TempleOS zealot with more zeal than I, might say we should save lines-of-code by removing the CISC optimizing.
