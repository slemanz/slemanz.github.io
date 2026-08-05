+++
title = "Hardware Gallery"
slug = "hardware"
description = "A look at some of the boards and prototypes I've designed and built."
date = "2026-03-01"
build = {list = "never", render = "always"}
+++

A look at some of the boards and prototypes I've designed and built, from concept sketches to working hardware.

This is what I enjoy the most: seeing something go from a schematic on screen to a physical board that actually does what it's supposed to do.

---

<!-- 
HOW TO ADD A NEW BOARD HERE:

1. Put the photos in static/images/hardware/
   Example: static/images/hardware/ecu-top.jpg

2. Copy the "Nina Project" block below, then change the title,
   the image path and the description.

3. Each section works well with 1-3 photos.
-->

### Nina Project: Data Acquisition Device

![3D render of the Nina board, with the u-blox NINA-B306 module, the SWD header, the micro-USB port and the expansion connector](/images/nina-project.png)

Complete hardware design for a data acquisition device based on the u-blox NINA-B306 (nRF52840). Designed in KiCad, from schematic to final board: power regulation, SWD debug header, USB and expansion connectors, all on a board small enough to fit in a pocket.

The firmware that runs on it lives in the [Nina Project repository](https://github.com/slemanz/nina-project).

---

### More boards coming soon

There's more on the bench: sensor acquisition boards, ECU prototypes and the debug setups behind them. Photos go up here as each one comes together.

---

> *"The hardware is the instrument; the firmware is the music."*

Want to see the code behind these boards? Check out my [Projects](/projects/) or visit my [GitHub](https://github.com/slemanz).
