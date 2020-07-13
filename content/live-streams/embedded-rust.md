---
title: "Series: Embedded Rust: Rust Discovery Book (STM32)"
subtitle: Introduction to Programming Minecraft Addons
comments: false
date: 2020-07-12T19:00:00-04:00
tags: ["Rust", "ARM", "STM32", "Embedded", "LiveStream"]
---
I've been a hobbyist with electronics for a number of years. Working on a project, then nothing for months (sometimes years). Then picking it back up. I've always wanted to gain more experience doing embedded development.

Recently i've been working on a project in Rust called [Krustlet](https://github.com/deislabs/krustlet) that allows Kubernetes to be used to orchestrate Web Assembly directly on the a node, without being put inside a container. [Brian Ketelsen](https://twitter.com/bketelsen) and I worked on a [talk and demo](https://www.youtube.com/watch?v=DWCrP41SjbM&feature=youtu.be&t=4091) for it where we used WASM to control a robotic arm. This got me excited about doing some embedded projects again. I also liked the idea of doing it with Rust.

Eventually i'd like to bring back my BBQ PID controller that controls a blower motor on my smoker to maintain temperature and some other projects i've started and not finished (E_TOOMANYPROJECTS). First i'm going to go back to the basics.

So, i've acquired an [STM32F3DISCOVERY](https://www.st.com/en/evaluation-tools/stm32f3discovery.html) board and am making my way through the Rust [Embedded Discovery](https://docs.rust-embedded.org/discovery/) book. I'll then my make my way to the [The Embedded Rust Book](https://docs.rust-embedded.org/book/index.html). 

## Archive

### Embedded Rust: Rust Discovery Book (STM32) Pt. 1
In this episode I set up my development environment and work on building, flashing, and debugging on board.
{{< youtube CnVIz4KVm8M>}}

### Embedded Rust: Rust Discovery Book (STM32) Pt. 2
Setup VS Code to debug using OpenOCD, solve the LED roulette challenge, working through Chapters 6-11. Ran into some issues doing ITM and USART. Which I'll try to solve in the next episode before moving on to bluetooth.
{{< youtube n079L79O4PY>}}