# Aleph-0 Requirements

## About the Name

Aleph-0 (written ℵ₀, pronounced "aleph naught") is the mathematical symbol for the
cardinality of the natural numbers — the smallest infinite cardinal. It is the simplest
infinity: the one you encounter first. The name reflects the spirit of this project: a
starting point, a foundation, the operating system you build when you are learning how
operating systems work.

In code and file names, the project is written `aleph-0` or `aleph0` as context requires.

## Purpose

Aleph-0 is an operating system designed to be built. It is the subject of a tutorial
series on operating system development in Rust, intended for developers who are ready to
go beyond application programming and understand how operating systems work from the
inside. The assumed reader has at least entry-level software engineering experience and
some familiarity with low-level development, though prior OS development experience is not
required.

The OS is real — it runs on real hardware and does real things. But every decision in its
design is made with a learner in mind. Where a more sophisticated approach would obscure
the lesson, we choose the simpler one. Where an interesting design choice teaches more
than the obvious one, we take it.

## Values

These values guide every design decision in Aleph-0. When they conflict, the order below
reflects priority.

1. **Educational value** — Aleph-0 exists to teach. A design that is harder to understand
   is a worse design, even if it is technically superior. Every non-obvious choice should
   illuminate something about how operating systems work.

2. **Simplicity** — Prefer straightforward designs. Avoid complexity that does not earn
   its place by teaching something worthwhile.

3. **Correctness** — The OS must work. A reference implementation that crashes, corrupts
   data, or behaves unpredictably undermines everything the tutorial is trying to teach.

4. **Safety** — `unsafe` Rust is sometimes unavoidable in OS development, but it should
   be minimized and clearly justified. Every `unsafe` block must document the invariants
   it relies on.

5. **Fun** — Building an operating system should be enjoyable. Aleph-0 should be a
   project people are glad they worked through.

## Goals

The following describe what Aleph-0 is as a finished product:

- A working monolithic kernel targeting x86-64 (PC) and AArch64 (Raspberry Pi 4)
- A clean architecture abstraction layer, making it straightforward to add support for
  new targets
- A userspace environment including a custom shell and support for userspace programs
- Rust `std` available to userspace programs, covering standard I/O, filesystem access,
  and basic IPC
- Support for keyboard input, framebuffer display, block storage, and serial/UART
- Well-documented subsystem APIs
- Subsystems that can be unit tested on the host operating system
- The ability to run in an emulator or virtual machine as well as on real hardware

## Non-Goals

The following are explicitly out of scope:

- **Production use** — Aleph-0 is not intended for production deployment and makes no
  stability guarantees
- **Performance optimization** — performance is not a priority beyond what is needed for
  the OS to function reasonably well
- **Security hardening** — security mechanisms are out of scope unless they serve an
  educational purpose
- **Complete `std`** — the Rust standard library implementation covers what is needed for
  the shell and simple userspace programs; completeness is not a goal
- **Broad hardware support** — only x86-64 PC and Raspberry Pi 4 are supported reference
  platforms
- **Mouse support**
- **Networking**
- **Audio**
- **POSIX compliance** — Aleph-0 does not aim to be POSIX-compliant, though some
  interfaces may resemble POSIX where that is the natural design

## About These Requirements

This document is the entry point for the Aleph-0 requirements. The full requirements are
organized across multiple documents by subsystem, linked below. Each document specifies
*what* the finished OS must do — not how the tutorial builds it step by step, and not
implementation details, which belong in the specification.

The fact that Aleph-0 is built as part of a tutorial informs these requirements: they
reflect a design chosen for clarity and educational value, not one optimized for
production use. Readers encountering design choices that seem simpler than necessary
should understand that simplicity is often the point.

1. [Architecture Abstraction](architecture-abstraction.md)
2. [Platform Support](platform-support.md)
3. [Devices](devices.md)
4. [Filesystem](filesystem.md)
5. [Process Model](process-model.md)
6. [Program Execution Environment](program-execution-environment.md)
7. [Rust `std`](rust-std.md)
8. [Shell and Utilities](shell-and-utilities.md)
