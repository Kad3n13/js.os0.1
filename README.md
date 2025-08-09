<h1>First Steps in BIOS Programming</h1>

<p><strong>BIOS Basics:</strong>  
- Occupies 512 bytes on disk, typically stored at memory address <code>0xFC00</code>.</p>

<p><strong>Initialization:</strong>  
- Set up the stack pointer (SP) by copying a value into register AX, then moving AX to SP.</p>

<p><strong>Printing a Message:</strong>  
- Use registers AX, BX, and possibly CX to prepare parameters.  
- Trigger a BIOS interrupt to display the message.</p>

<p><strong>Halting the Computer:</strong>  
- Disable interrupts.  
- Issue the halt interrupt.  
- Enter an infinite loop to prevent further execution.</p>

<p><strong>Notes on Data:</strong>  
- Example binary patterns:  
  <code>01011100 01011100</code> (hex <code>0x5C5C</code>)  
  <code>11111111 00000000</code> (hex <code>0xFF00</code>)</p>


<img width="1918" height="1029" alt="image" src="https://github.com/user-attachments/assets/b7ab974f-3026-43da-9f16-e3139900224f" />

# j.os.s - Minimal 16-bit JavaScript OS Bootloader

<p align="center">
  <img src="https://img.shields.io/badge/Language-JavaScript-yellow.svg" alt="JavaScript" />
  <img src="https://img.shields.io/badge/Platform-x86_16--bit-blue.svg" alt="16-bit x86" />
  <img src="https://img.shields.io/badge/Status-Experimental-red.svg" alt="Experimental" />
</p>

---

## Overview

`j.os.s` generates a 512-byte BIOS boot sector binary via JavaScript, targeting 16-bit x86 real mode.  
Demonstrates CPU setup, BIOS interrupts, and bootloader basics.

---

## Features

- 16-bit real mode boot sector  
- Stack pointer initialized to 0xFBFF  
- Prints message via BIOS interrupt 0x10 (teletype)  
- Disables interrupts and halts CPU safely  
- Infinite halt loop with short jump  
- Pads to 510 bytes + boot signature 0xAA55  

---

## Technical Details

- Origin at memory 0xFC00  
- Machine instructions encoded as hex strings  
- Uses BIOS int 0x10 for output  
- CLI disables interrupts before halt  
- Boot signature appended to last 2 bytes  

---

## Assembly snippet (conceptual)

asm
bits 16
org 0xfc00

halt_loop:
    nop
    hlt
    jmp halt_loop
****

<h>Usage</h>
<p>node main.js <output-file></p>
<h>Example</h>
  <p>node main.js boot.bin></p>
  <h6>Generates a 512-byte bootloader binary with the custom message</h6>
<h>package.json</h>
  <p>{
  "name": "j.os.s",
  "version": "0.0.1",
  "type": "module",
  "main": "main.js",
  "scripts": { "start": "node ." },
  "keywords": ["javascript", "operating system", "bootloader", "osdev"],
  "author": "0x40.8p0",
  "license": "UNLICENSED"
}</p>
<h>Workflow</h>
  <ul>
    <li>Initialize SP = 0xFBFF</li>
    <li>Print string using BIOS teletype interrupt</li>
    <li>Disable interrupts (cli)</li>
    <li>Halt CPU (hlt)</li>
    <li>Loop indefinitely (jmp)</li>
    <li>Pad remaining bytes with NOPs</li>
    <li>Append boot signature 0xAA55</li>
  </ul>
<h>Notes</h>
  <ul>
    <li>Educational, experimental</li>
    <li>Testable in QEMU/Bochs</li>
    <li>Not a full OS, just a bootloader foundation</li>
  </ul>
<h>License</h>
  <p>Unlicensed — modify and experiment freely.</p>
<h>Contact</h>
<h6>Author: 0x40.8p0</h6>
<h6>Open issues or contribute anytime.</h6>
<h6><p align="center"><em>Built with ❤️ and JavaScript assembly magic.</em></p> ```</h6>
