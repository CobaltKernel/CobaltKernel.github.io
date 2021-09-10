---
title: Kernel Foundations
---




# CobaltOS - Kernel Foundations

----

## Motivation

The main motivation for this project is to create a simple 64-bit x86 Kernel, complete with a Terminal, Filesystem, Shell, Text Editor, Assembler.

## Design Goals

- Simple & Robust.

- Partially Self-hosting.

## Kernel Design Patterns

- Monolithic Kernel - Modules are built-in to one binary.

## Language Choice

- Rust - Memory Safety, High-level, vast array of library available.

----

## Booting The System

The first responsibility of a Kernel is made up of 3 parts:

1. Enable the A20 line to be able to use more than 64KB of memory, setup the VGA graphics mode.
2. Load in the rest of the Kernel using the **INT 0x13, AH=0x42** BIOS Function.
3.  Switch from **real** mode to **protected** mode & Call the kernel's main function.

In the case of CobaltOS the process of booting the system is handled by the 'Bootloader' crate & Bootimage, provided by Philip Opperman. This handles a huge amount of the heavy lifting that needs to be done.

----

## Using Rust Core

Thankfully, Rust is built with the purpose of freestanding development, and as such, the freestanding parts of the rust standard library can be automatically built as part of the boot process, and parts that rely on memory allocation can be used by setting the **Global Allocator** using the **#[global_allocator]** attribute on a struct that implements the **GlobalAllocator** trait.

----

## Setting up an output system

The x86 Platform provides two ways of outputting & displaying information to the user, VGA & the Serial Ports. Cobalt initially uses the Serial Port to print to a *'remote'* terminal, VGA textmode is currently in the works.

----





