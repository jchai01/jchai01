+++ 
date = 2024-04-25T00:03:12+01:00
title = "Why x86 needs to die, summary"
description = ""
slug = ""
authors = []
tags = ["blog"]
categories = []
externalLink = ""
series = []
+++

This blog is a compilation of summaries and insights gathered from [ this video by ThePrimeagen ](https://www.youtube.com/watch?v=xCBrtopAG80), where he reacts to an article titled [ "Why x86 needs to die" ](https://hackaday.com/2024/03/21/why-x86-needs-to-die/) together with hardware expert Casey Muratori. A [ counter-article ](https://chipsandcheese.com/2024/03/27/why-x86-doesnt-need-to-die/) is also available at [ Chip and Cheese ](https://chipsandcheese.com/), a site that blogs about micro analysis stuff, and it's recommended by Casey.

# Why are register names so weird? (4:35)

In assembly language, general purpose register names from the second half made sense (named r8, r9, r10, r11 ...) but not the first half (they are not named r0, r1, r2 ...) because original 8000 series CPUs started out with four registers: A, B, C, and D. From there, it evolves as the bit increases. Let's take register A, for example:

- 8-bit CPU: A
- 16-bit CPU: AX, also known as A Extended, has 2 parts (AL and AH, which stand for low and high, respectively).
- 32-bit CPU: EAX, bottom 16 bits can be accessed with AX. EAX gives you the full 32-bit.
- 64-bit CPU: RAX

# Why little endian? (8:55)

Endianness refers to byte order, not bits. Network byte order uses big endian, which is the natural way in which humans read something (left to right), where the most significant bytes are read first. Almost all hardware uses little endian (opposite of big endian).

Casey's explanation goes something along the lines of:
If we have an address of a particular byte position in memory, the address stays the same no matter how big the value that it is pointing to gets, but this is not the case for big endian as it "grows in the other direction."

# Supporting 8086 real mode isn't a big deal (10:30).

Virtual address space did not exist back then, and direct memory addresses were used (which is what 8086 real mode in modern x86 does). Virtual address spaces don't necessarily map to physical RAM, and this gives modern CPUs many features, such as swapping processes. Casey argues that there are not really additional things to do to support direct physical addressing and that the original author could pick a better complaint, such as having to have more "segment registers.".

Prime points out that the article sounds legit due to software usually being worse when trying to support backward compatibility; he used NodeJS vs. Bun as an example, saying Bun has better performance as it ignores supporting backward compatibilities. Casey mentioned that it's not the case for hardware. x86 gives you both the fast performance of "Bun" and, whenever it can't, the slow emulation of "NodeJS" if needed.

# Von Neumann architecture (14:30)

A CPU with a Von Neumann architecture would have the program code and program data residing in the same address space. Von Neumann is considered to be the greatest computer science person.

- Prime recommends the novel "Three Body Problems.".
- Casey mentions a famous biography of him called "The Man from the Future.".

# CPU execution breakdown (18:22)

A single instruction, for example, add, does not equate to doing one operation. It could be broken down into many operations known as micro-ops. Casey mentions that all modern processes use micro-ops; even RISC architectures such as ARM do not always map instruction to operation one to one.

## Why an instruction may seem like it only takes one clock cycle to complete: pipelining (24:40)

Casey gave an example where the ADD instruction takes 14 clock cycles to complete. The clock rate has to be slowed down in order for it to complete in 1 clock cycle, as there is a limit to how much can be accomplished in 1 clock cycle. We want to maintain high clock rates so the stages of ADD are overlapped (fetching, decoding, turning it into micro-ops, etc.).

Imagine putting an ADD instruction on every clock cycle. After 14 clock cycles, each clock cycle returns the result of ADD, making it seem like only 1 clock cycle is needed.

## CPU pipelining, washer and dryer analogy (26:50)

An example of how the CPU utilizes micro-ops to maximize each clock cycle. Which one is better?
- washer and dryer as one unit, which takes 2 hours to complete.
- washer and dryer as separate units, which takes 1 hour to complete each task.

It doesn't matter as both take 2 hours, right? Wrong! (from a CPU standpoint)
While the clothes are in the dryer, a second batch of clothes can be placed in the washer. 2 batches of clothes now took 3 hours instead of 4.

## Out-of-Order Execution and Superscalar (28:25)

Out of order, execute micro-ops in a non-sequential manner if they are independent of each other. Superscalar just means executing multiple micro-ops at once. 

# Speculative Execution, Spectre and Meltdown (30:48)

Speculative execution runs the code in the IF branch before knowing if the IF statement results in true. The state of the program is reversed if it's false. 

Casey mentioned that spectre and meltdown are caused by speculative execution, but the M2 bug has nothing to do with speculative execution; branch-free code will still be hit by the M2 bug. It is caused by the memory prefetcher.

# Address Generation Unit (AGU) (33:20)

When memory access is needed, an effective address calculation takes place to figure out where to get the memory from. The number of AGUs determines how many memory fetches can be issued per clock cycle. If you have three AGUs, you can issue three reads in one cycle.

# Arithmetic Logic Unit (ALU) (34:50)

In a modern CPU, the ALU has a list of operations it can do, e.g., a particular operation can do integer multiplication. They are optimized for specific operations (XOR, multiply, etc.), as shown in uops.info. 

# uops.info (35:40)

[uops.info](http://uops.info) shows the different lists of operations in the ALU. For example, under tables->search for ADD, it shows a list of all the permutations there are for ADD.

- ADD(R32, R32): Add a 32-bit register to another 32-bit register.
- ADD(R32, M32): Fetch the value located at memory location M32 and add it to the 32-bit register. (I think that's what he meant.)
- ADD(M64, I8): 64-bit memory location, added to an 8-bit immediate value.

Over at the port section of the table, an example shows ADD (M64, I8):

ADD(M64, I8) -> 1*p0156B+1*p23A+1*p49+1*p78

- The "0156" portion shows the port number on which the ALU/AGU can perform these micro-ops. In this case, port numbers 0, 1, 5, and 6 have the ADD unit on them. At any given clock cycle, there are four ports to choose from.
- The + symbol separates the micro-ops. This instruction takes 4 micro-ops.
- Micro-ops pile up, waiting for the scheduler (a chip has multiple schedulers) to place them in the appropriate ports. Out-of-order execution is implemented here.

# Number of instructions supported is not a big deal (45:30)

CPUs are divided into many parts now; the fetch decode execute cycle that generates those micro-ops (AKA frontend) is independent from the "backend," and adding more instructions does not affect the actual execution engine of the CPU at all. It does matter a little, but it depends on how specific the permutations are.

# Why certain oddball features exist in the CPU (48:35)

Casey mentions the support of critical features such as video compression/decompression and AI processing, implementing them at the hardware level improves performance, and Intel has customers that would greatly benefit from them. He mentions that RISC-V would end up in the same boat as Intel x86 processors in terms of complexity if they were to implement those mentioned features too, and extensions such as "RISC-V-video-decompression" would exist. 

# "8086 is simple" misconception (49:45)

Every single instruction is microcoded in 8086. It is not simple.

# Why is the term "die" used? (50:40)

Casey has no idea either, but he can tell you what it is: chips are being manufactured with a litographic process where photons are being shot at a wafer of silicon. When it’s cut out, it’s called the die. Could be from the word diecast.

# What actually matters? Decoding complexity (55:48 - end)

- Casey states that RISC-V is popular because it's free, not because of its simplicity. ARM is better than RISC-V in terms of simplicity; if RISC-V features were extended to match ARM, both chips would be similar.
- Superscalar, out-of-order, and speculative execution are not unique to x86. All modern CPUs are using them, including the ARM chips in our phones.

Casey mentions that decoding complexity is a valid argument and has nothing to do with RISC vs. CISC. Instructions for the x86 are encoded badly due to legacy or bad choices that were inherited, and decoding these instructions is the bottleneck. All modern x86 chips are taking up more space for decoding than they should, and Intel already has proposals to fix these encoding issues.

# My take

The main advantage of RISC architecture is its efficiency, which leads to low power consumption. This improves battery life, and fans are no longer required due to the low heat output.

If the above-mentioned decoding complexity is somehow resolved for x86/x64, will it match the efficiencies of, say, the ARM or M1 chip? Or will the opposite occur? RISC architecture gains popularity and starts to support more features for compatibility reasons; complexity grows, and eventually it matches CISC architecture chips in terms of efficiency.
