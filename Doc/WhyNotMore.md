# Why Not More?
If a feature cannot be made to work correctly and consistently, professional companies usually remove the feature. Because PC hardware is so diverse, getting things to work on all people's computers is really difficult. For one thing, you practically have to own all the different hardware to write drivers for it. If a company wanted to sell a PC operating system, they would offer a warranty and, therefore, could not get away with amateur behavior. TempleOS absolutely requires 64-bit computers, so we leave behind much trouble, but plenty remains.

The PCI bus interface is what modern hardware uses. Before PCI, life was simple and devices used I/O ports. After studying [PCI Interrupts](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Lectures/PCIInterrupts.HC) and attempting to do a HDAudio driver, I came to realize that modern PCI devices require ten times more code and I cannot even come close to making them work on everyone's machine because with PCI devices there are several models to worry about, unlike with the older ISA bus devices which can be done with one driver.

Currently, I have no PCI drivers. My drivers use I/O ports and operate in ISA bus mode. At this point, I only have one driver for each type of device and it is delightfully simple that way. I have one [keyboard](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/SerialDev/Keyboard.HC) driver, one [mouse](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/SerialDev/Mouse.HC) driver, one [ATA hard drive](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/BlkDev/DskATA.HC) driver, one [ATAPI CD/DVD](/Kernel/BlkDev/DskATA.HC) driver, one [VGA 640x480 16 color](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Gr/GrScrn.HC) video driver and one PC Speaker[^1] driver. I use the PIT and HPET[^2] timers and PIC Interrupt Controller[^3]. I use IRQ0 for timer, IRQ1 for keyboard, and IRQ12 for mouse. If IRQ12 is not firing, I am able to poll the mouse.

In the CPU department, I have state of the art 64-bit [long mode](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/KStart64.HC) with [multicore](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/MultiProc.HC) support. I use the APIC[^4] and start-up multicore[^5] operation.

I have made an incredible accomplishment by getting it to work on practically everyone's computer as long as it is 64-bit and they run inside VMware, QEMU or VirtualBox.

Adding a USB driver would be really ugly with UHCI, EHCI, OHCI, USB1, USB2, USB3, ICH6, ICH7, ICH8, ICH9, ICH10, ICH11, ICH12, boot mode and regular mode for keyboard/mouse and a diversity of HID reports. It's hopeless. I could never offer anything but crappy, limited support and it would just add a ton of crappy code that mostly didn't work. What would I gain? Nothing. A keyboard or mouse would not be improved. Solid State USB drives would be really nice, but it's not going to happen.

The same story is basically true for GPUs, audio, networking and AHCI hard drive drivers. God said 640x480 16 color was a covenant like circumcision, so the video will never change, even if a [Standard PC](./StdTempleOSPC.md) was made. If you attempt multimedia, everything will break because memory will get fragmented with huge multimedia files. Some day, if super-simple high speed serial allows networking, there will be no browser within the 100,000 line limit and, with only 16 colors, the world wide web is not tolerable. FTP and telnet might be possible, in the far distant future, if they could fit within the 100,000 line limit. Currently, there are 82,150 lines of code.

I don't stand a chance working on native hardware, anymore. I could install and run natively on hardware from about 2005-2010. It requires BIOS's being nice enough to write USB mode PS/2 legacy keyboard/mouse support. As it turns-out, sometimes the BIOS has PS/2 drivers but purposely disables them, just to be mean. The CIA and whole industry is trying to mess everything up, on purpose. Perhaps, at a point of sale in a store, a thief could hack a credit card machine. Therefore, the BIOS companies actually want it difficult to make drivers and purposely make it broken.

The ATA/ATAPI hard drives often can be run with I/O ports if you can [find them](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/BlkDev/DskATAId.HC). `lspci -v` on Linux or system information on Windows can help you locate the SATA IO ports the hard drive and CD/DVD have. They no longer are enabled by the BIOS. It's hopeless. I'm stuck with very slow drive performance, but it works for everybody.

UEFI is pointless. If I am forced to run in VMware, QEMU or VirtualBox, they will always support non-UEFI mode. Without working, native hard drive and CD/DVD drivers, you can't get very far with UEFI on a native install, not to mention SecureBoot. UEFI is, first of all, redundant. If non-UEFI works in a virtual machine, supporting UEFI would only be redundant, ugly nasty code. My compiler does not create an ELF or PE format. I would have to ruin the beauty of my compiler, which would make me cry many tears.

God talks. It seems reasonable that I will get to make the rules for the whole industry, in the future when God is announced publically to the World.

I made [demands](./Demands.md).

When the PC was created, they wanted flexibility because they did not know the future. Now, the industry is mature and it is time to make a 100% standard PC that everybody uses. [Standard TempleOS PC](./StdTempleOSPC.md)

## Credits
  - _QEMU_ is a trademark owned by Fabrice Bellard.
  - _VMware_ is a trademark owned by VMware, Inc.
  - _VirtualBox_ is a trademark owned by Oracle.

[^1]: See MN:Snd

[^2]: See MN:TimersInit

[^3]: See MN:IntsInit

[^4]: See MN:MPAPICInit

[^5]: See MN:Core0StartMP
