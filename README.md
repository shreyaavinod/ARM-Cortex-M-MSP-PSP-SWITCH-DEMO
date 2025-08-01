# STM32 Cortex-M4: PSP Stack Switch and SVC Handler (Bare-Metal)

This project demonstrates how to switch the stack pointer from the default **MSP** (Main Stack Pointer) to **PSP** (Process Stack Pointer) in **thread mode**, and then generate a **Supervisor Call (SVC)** exception in **bare-metal STM32** programming (no RTOS used).

---

## 🧠 Overview

- Uses **inline assembly** and `__attribute__((naked))` functions to:
  - Initialize and switch to PSP.
  - Trigger a software interrupt using `SVC #2`.
- Implements an **SVC_Handler** that executes when the exception is triggered.
- The stack is divided manually:
  - Top 128KB of SRAM (0x20000000 to 0x20020000) is split between MSP and PSP.
  - PSP is allocated the final 512 bytes just below `SRAM_END`.

---

## Memory Layout 
```
SRAM Start       : 0x20000000
SRAM Size        : 128 KB
SRAM End         : 0x20020000

PSP Region Start : 0x2001FE00
PSP Region End   : 0x20020000
```
