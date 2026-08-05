+++
title = "Projects"
slug = "projects"
+++

Here are some of the projects I've been working on. All bare-metal, all from scratch.

---

### [Hardware Gallery →]({{< ref "projects/hardware" >}})

Photos of boards, prototypes and debug setups I've designed and built. From schematic to working hardware.

---

### [Blinky to Bootloader](https://github.com/slemanz/blinky-to-bootloader)

![The project running on an STM32F411 black pill, with the LED, the ST-Link probe and the UART wiring on the breadboard](/images/blinky-to-bootloader.png)

What started as a simple LED blink evolved into a complete STM32F411 application with a 5-layer architecture and a UART-based bootloader for firmware updates. Everything bare-metal, everything Makefile.

**Stack:** C, ARM Cortex-M4, STM32F411, Makefile, Python (DFU tool)

---

### [RA4M1 Sandbox](https://github.com/slemanz/RA4M1-sandbox)

Bare-metal firmware environment for the Renesas RA4M1 (Arduino UNO R4 Minima). No Arduino framework, no CMSIS: direct register manipulation, J-Link debugging, clean layer separation.

**Stack:** C, Renesas RA4M1, Makefile, J-Link/Ozone

---

### [Nina Project](https://github.com/slemanz/nina-project)

![3D render of the Nina board, with the u-blox NINA-B306 module, the SWD header, the micro-USB port and the expansion connector](/images/nina-project.png)

Hardware and firmware for a data acquisition device built around the u-blox NINA-B306 (nRF52840). A full product development cycle, from schematic to working board and firmware.

**Stack:** C, nRF52840, KiCad, Makefile

---

### [Advanced Embedded C](https://github.com/slemanz/advanced-embedded-c)

Study repository covering design patterns, optimized patterns, data structures, build systems, bootloader concepts, safety, fault handling and TDD, all applied to embedded C.

**Topics:** Design Patterns, FSM, TDD, Build Systems

---

More projects on my [GitHub](https://github.com/slemanz).
