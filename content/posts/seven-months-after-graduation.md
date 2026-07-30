+++
authors = ["William Sleman"]
title = "Seven Months After Graduation"
date = "2026-03-19"
description = "On what happens when you stop studying for exams and start studying for yourself."
tags = [
    "career",
    "embedded",
    "personal",
    "learning",
]
categories = [
    "personal",
]
+++

I graduated in Electrical Engineering seven months ago. And I think I've learned more in these seven months than in any single year of college.

That's not a criticism of university. It gave me the foundation, the vocabulary, the way of thinking. But there's something different about learning when no one is grading you. When there's no exam next week. When the only reason you're reading a datasheet at 11 PM is because you genuinely want to understand how a DMA controller arbitrates bus access.

<!--more-->

## The shift

In college, I studied to pass. I'm not proud of it, but it's honest. There were subjects I loved (anything related to microcontrollers, circuit design, embedded systems) and subjects I endured. The system rewards you for being good enough across the board, not for going deep in the things that matter to you.

After graduation, that changed. Not overnight, not dramatically. But slowly I noticed that my evenings looked different. Instead of watching something forgettable, I was reading reference manuals. Instead of dreading Monday, I was excited to get back to a firmware problem I'd been chewing on over the weekend.

I started dumping everything I learned into GitHub. Not polished projects with perfect READMEs, just raw knowledge. Driver notes, architecture experiments, design pattern implementations, assembly exercises. A brain dump in code form. The idea was simple: if I can implement it, I understand it. If I can't, I don't. No fooling myself.

## The books that shifted something

Two books hit me harder than I expected this year.

The first was *Talent is Overrated*. The core idea is almost uncomfortable: what we call talent is mostly the result of deliberate practice. Not just doing something repeatedly, but doing it with intention, pushing at the edges of what you can do, getting feedback, adjusting. The people we admire, the ones who seem gifted, usually just started earlier and practiced smarter.

That reframed everything for me. I used to look at senior engineers who could debug a timing issue from the waveform alone and think "I'll never be that good." Now I think "they've been doing this for fifteen years, and if I practice deliberately, I can get there too." It's not a guarantee. But it's a path, and that's enough.

The second was *How Einstein Ruined Physics*. Despite the provocative title, it's really about the danger of theoretical elegance replacing experimental truth. About how physics, after Einstein, became increasingly obsessed with beautiful mathematical frameworks that no one could test. The book argues that real understanding comes from engaging with the messy, physical world, not from building theories in isolation.

That resonated with me more than any engineering textbook ever did. Because embedded systems are the messy, physical world. Your code doesn't run in a mathematical abstraction. It runs on silicon that has temperature drift, on buses that have propagation delays, on power supplies that ripple. You can't just theorize about a bootloader. You have to flash it, watch it fail, read the fault registers, and figure out why your vector table offset was wrong.

I don't want to be the kind of engineer who hides behind abstractions. I want to be the kind who understands what's underneath.

## What the days look like now

I wake up, go to work, design ECUs and sensors, write firmware, run tests. I come home to the apartment I share with my girlfriend, the person who makes all of this sustainable. She's the reason I can spend an evening deep in an ARM architecture manual without feeling like I'm neglecting the things that matter. Because she *is* one of the things that matter, and she's right there, living her own passions alongside mine.

There's something about building a life with someone while building yourself as an engineer. The two things feed each other. Stability at home gives you the energy to push at work. Growth at work gives you confidence that spills into everything else.

After dinner, I usually open a terminal. Some nights I'm writing a driver for a peripheral I've never used. Other nights I'm refactoring something I wrote last month that I now realize was wrong. Sometimes I just read: datasheets, application notes, other people's code.

And then I push it to GitHub. Not because anyone's watching. But because putting it out there forces me to be honest about whether I actually understand it.

## The uncomfortable truth

I'm not where I want to be. Not even close. There are engineers out there who can read a schematic and immediately see the noise path I'd miss. Who can write an interrupt handler that I'd take three tries to get right. Who have an intuition about hardware that I'm still developing.

But seven months ago, I couldn't do half of what I can do now. And seven months from now, I'll look back at today the same way.

That's the thing about deliberate practice. Progress is slow enough that you don't notice it day to day. But when you zoom out and compare the code you wrote in January to the code you write in March, the difference is undeniable.

## What I know now

University taught me *what* things are. These seven months are teaching me *why* they work.

I know that a bootloader isn't magic. It's a piece of code that lives in a protected region of flash, validates an image, and modifies the vector table before jumping. I know that because I built one.

I know that a layered architecture isn't academic overhead. It's the difference between a project that scales and one that collapses under its own weight. I know that because I've experienced both.

I know that reading the datasheet isn't optional. It's the job. The peripheral doesn't care about your assumptions. It does exactly what the reference manual says it does, and when something goes wrong, the answer is always in there.

And I know that none of this came from talent. It came from sitting down, every day, and doing the work.

---

Seven months. It's not a long time. But it's long enough to know that I'm on the right path.

Not because someone told me. Because I can feel it.
