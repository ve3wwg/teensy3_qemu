teensy3_qemu
============

Changes to QEMU to accomodate the teensy3.x arm platform (Cortex-m4)

The 2.0.0 release of QEMU comes close to being useful for emulating
the teensy-3.x platform, using the lm3s6965evb machine (Stellaris
LM3S6965EVB). This board definition supports 256K flash, 64K SRAM
and supports the Cortex-m3 arm CPU. However, the SRAM component is
located at the incorrect offset for the Cortex-m4 (Freescale K20).

This repository of code changes are my attempt to support the teensy-3.1
specifically, with a view to building up Cortex-m4 support in the
future.

An early patch experiment solved the SRAM starting offset problem, by
patching the Stellaris machine. But in this repo, I'll be creating a
separate teensy3 machine to properly reflect a different machine and to
improve future maintenance.

CURRENT STATUS:
======================================================================

Fri Apr 18 09:32:44 2014

Using the machine name 'teensy-3.1' you now get a ARM CPU with the
static ram in the correct place (address 0x1FFF8000 for 64K). The
CPU emulation otherwise remains a Cortex-m3.

QEMU Command:
-------------

$ /usr/local/bin/qemu-system-arm -machine teensy-3.1 -nographic -monitor null -serial null -semihosting -kernel ./myarmprog.elf -gdb tcp::51234 -S

GDB:
----

$ arm-none-eabi-gdb --exec="myarmprog.elf" --se="myarmprog" --ex="target remote localhost:51234" --ex "load" -ex "b main"

Startup remains tricky, in gdb you must:

1.  set $sp = *0
2.  set $lr = -1
3.  b ResetHandler
4.  j ResetHandler

From there you can single step (si) or whatever. A useful view in
assembler is:

5. layout asm
6. layout regs

--
