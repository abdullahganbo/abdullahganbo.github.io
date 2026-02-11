# STM32F303 Minimum Viable MCU Board

## Objective
Design a minimal STM32 board to validate first-principles MCU bring-up,
including power, clocking, reset, and programming, without relying on
development boards.

## System Overview
- MCU: STM32F303CCT6
- Power: 3.3 V regulation
- Clock: External crystal oscillator
- Programming and debug: SWD
- Form factor: 2-layer PCB

## What I Designed
- Complete schematic including power, BOOT configuration, NRST, and SWD
- 2-layer PCB layout with grounding and decoupling strategy
- GPIO breakout for rapid validation and firmware testing

## Key Engineering Decisions
- Used an external crystal to ensure clock stability and control
- Kept the design minimal to expose bring-up issues early
- Chose a 2-layer board to prioritize manufacturability and clarity

## Issues and Lessons Learned
- Solder mask clearance around MCU pins was tight and will be relaxed in Rev B
- Decoupling placement can be improved to shorten high-frequency current loops

## Status
Design completed. DRC/ERC clean. Fabrication pending.

