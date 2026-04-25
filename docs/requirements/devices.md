# Devices

Covers the I/O devices Aleph-0 supports: keyboard input, framebuffer display, block
storage, and serial/UART communication.

## Overview

Aleph-0 supports a fixed set of devices, with the specific hardware varying by platform.
The table below summarizes the supported device for each platform and device class.

| Device | x86-64 | AArch64 (QEMU) |
|--------|--------|----------------|
| Serial/UART | 16550A (COM1) | PL011 |
| Framebuffer | Limine-provided | Limine-provided |
| Keyboard | PS/2 (i8042) | VirtIO |
| Block storage | AHCI | VirtIO block |
| System timer | APIC timer | ARM generic timer |

## Serial/UART

Aleph-0 supports one serial port per platform, used for kernel logging and debug output.
Serial is not a user-facing console; it is not possible to run the shell or interact with
the OS over serial.

On x86-64, the 16550A-compatible UART at COM1 is used. On AArch64 QEMU, the PL011 UART
is used.

## Framebuffer

Aleph-0 supports a single framebuffer display provided by the Limine bootloader. The
kernel does not initialize display hardware directly.

## Keyboard

Aleph-0 supports a single keyboard for user input.

On x86-64, keyboard input is provided by a PS/2 keyboard via the i8042 controller. On
AArch64 QEMU, keyboard input is provided by a VirtIO keyboard device.

## Block Storage

Aleph-0 supports block storage devices for use by the filesystem.

On x86-64, AHCI is used for both real hardware and QEMU emulation. On AArch64 QEMU, a
VirtIO block device is used.

NVMe is not supported. On x86-64 machines without SATA, Aleph-0 must be run in a
virtual machine using QEMU's AHCI emulation.

## System Timer

Aleph-0 requires a hardware timer for preemptive scheduling and timekeeping.

On x86-64, the APIC timer is used. On AArch64, the ARM generic timer is used.
