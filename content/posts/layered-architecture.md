+++
authors = ["William Sleman"]
title = "How I Structure My Embedded Projects"
date = "2026-03-15"
description = "A practical look at the 5-layer architecture I use in bare-metal firmware."
tags = [
    "embedded",
    "architecture",
    "firmware",
    "C",
]
categories = [
    "embedded systems",
]
+++

Every firmware project I start follows the same structure. Not because I'm rigid about it, but because after enough projects, you learn that a clean architecture saves you more time than it costs.

<!--more-->

## The problem

Most embedded projects start small. A single `main.c` file, a few register writes, a blinking LED. But then features creep in: UART communication, a timer interrupt, an ADC reading, a protocol parser. Before you know it, your 200-line file is 2000 lines and everything depends on everything else.

I've been there. And the solution I settled on is a **5-layer architecture**:

```
┌────────────────┐
│      APP       │
├────────────────┤
│     COMMON     │
├────────────────┤
│   INTERFACE    │
├────────────────┤
│    DRIVERS     │
├────────────────┤
│    HARDWARE    │
└────────────────┘
```

## The layers

**App**: the application logic. This is the only layer that knows what the product *does*. It calls the common layer for services but never touches a register directly.

**Common**: shared services like communication protocols, BSP (Board Support Package) and core utilities. This layer provides abstract APIs that the app consumes.

**Interface**: the bridge between Common and Drivers. This is what makes it possible to swap microcontrollers without rewriting the whole project. The interface defines *what* needs to happen; the drivers define *how*.

**Drivers**: hardware-specific implementations. All the register-level code lives here: GPIO, UART, SPI, timers. This is the layer that reads datasheets.

**Hardware**: the physical MCU and its peripherals. Not code, but the thing your code talks to.

## Why it works

The key insight is that **each layer only talks to the layer directly below it**. The app never calls a driver function. A driver never includes an app header. This makes every layer independently testable and replaceable.

When I ported my [Blinky to Bootloader](https://github.com/slemanz/blinky-to-bootloader) project to a different MCU, I only had to rewrite the Drivers layer. Everything above it (the bootloader logic, the UART protocol, the DFU process) stayed exactly the same.

That's the payoff. The extra 30 minutes you spend setting up the structure saves you days when the project grows.
