# Platform Support

Describes the supported hardware platforms, their boot processes, and
platform-specific behavior.

## Supported Platforms

Aleph-0 targets two platforms:

- **x86-64 PC** — supports both emulation and real hardware
- **AArch64** — emulation only, via QEMU

Both platforms boot via the [Limine](https://github.com/limine-bootloader/limine)
bootloader from a hybrid ISO image, bootable from either an optical disc or a USB drive.
Installation to a system disk is out of scope.

## x86-64 PC

### CPU Requirements

- x86-64 architecture
- APIC (Advanced Programmable Interrupt Controller) required
- ACPI required

### Memory

Aleph-0 guarantees correct operation with between 1 GiB and 16 GiB of RAM. Behavior
outside this range is unspecified.

### Symmetric Multiprocessing

Aleph-0 supports SMP on x86-64. All logical CPUs present in the system may be used by
the kernel.

### Boot

x86-64 systems may boot via UEFI firmware or legacy BIOS. In both cases, Limine loads
the kernel from the hybrid ISO image.

## AArch64 (Emulation Only)

AArch64 support is provided through QEMU's `virt` machine. Running Aleph-0 on AArch64
real hardware is not supported.

### Memory

Aleph-0 guarantees correct operation with between 1 GiB and 16 GiB of RAM configured
for the virtual machine.

### Symmetric Multiprocessing

Aleph-0 supports SMP on AArch64. All virtual CPUs configured for the QEMU instance may
be used by the kernel.

### Boot

AArch64 boots via UEFI firmware (OVMF/EDK2). Limine loads the kernel from the hybrid
ISO image.

## QEMU Testing Support

Both platforms support the following mechanisms for automated testing under QEMU:

- **Serial output** — the kernel may write test results to the serial port, which QEMU
  exposes to the host
- **Programmatic exit** — the kernel may signal test pass/fail and exit QEMU with a
  status code:
  - x86-64: via the `isa-debug-exit` device
  - AArch64: via semihosting
