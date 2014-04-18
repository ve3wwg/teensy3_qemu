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

Stay tuned. Fri Apr 18 07:59:24 2014
