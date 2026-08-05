+++
authors = ["William Sleman"]
title = "Why I Write Bare-Metal Firmware"
date = "2026-03-01"
description = "On choosing to understand the hardware instead of hiding from it."
tags = [
    "firmware",
]
categories = [
    "embedded systems",
]
+++

There's a quote I think about often: *"If you wish to make an apple pie from scratch, you must first invent the universe."* It's from Carl Sagan, and while he was talking about cosmology, I think it applies just as well to embedded systems.

<!--more-->

When I started working with microcontrollers, the first thing everyone told me was to use a HAL. Use the IDE. Generate the code. Click the buttons. And it works. I'm not going to pretend it doesn't. But I never felt like I understood what was happening.

So I went the other way. I started reading reference manuals. I wrote my own startup code. I configured the clock tree by hand. I set up UART by writing to registers directly. It took longer, but when something went wrong, I knew *exactly* where to look.

That's the thing about bare-metal: it's not about being difficult for the sake of it. It's about removing the layers between you and the hardware so you can actually reason about what's happening. When your bootloader doesn't jump to the application, you need to understand the vector table. When your DMA transfer corrupts data, you need to know about memory alignment. No amount of HAL abstraction will teach you that.

I'm not against frameworks or HALs. They have their place, especially in production environments with tight deadlines. But I believe that to use them well, you first need to understand what they're doing for you. And the only way to get there is to do it yourself at least once.

That's why most of my projects start with a Makefile, a linker script, and a blank `.c` file. Not because I enjoy suffering, but because I enjoy understanding.
