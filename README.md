# MINT64 OS Study

『64비트 멀티코어 OS 원리와 구조』를 중심으로 운영체제를 직접 구현하며 공부하는 개인 학습 프로젝트입니다.

## Goal

완성된 OS를 빠르게 만드는 것보다 다음을 목표로 합니다.

* x86/x86-64 시스템의 부팅 과정을 이해한다.
* BIOS, Bootloader, CPU Mode 전환 과정을 이해한다.
* GDT, IDT, Paging, Interrupt 등의 동작 원리를 이해한다.
* Memory Management, Task, Scheduler, Context Switch를 직접 구현하며 학습한다.
* Multicore 및 SMP 구조까지 전체 OS 흐름을 이해한다.
* 코드가 동작하는 것에서 끝나지 않고 각 코드가 왜 필요한지 설명할 수 있도록 한다.
* 개발 과정의 시행착오와 디버깅 과정을 Git과 DEVLOG에 기록한다.

## Environment

* Host: Apple Silicon MacBook / macOS / ARM64
* Target: x86 / x86-64 Bare Metal
* Emulator: QEMU
* Assembler: NASM
* Compiler: x86/x86-64 ELF Cross Compiler
* Build: Make
* Version Control: Git

## Main Reference

* 『64비트 멀티코어 OS 원리와 구조』

교재의 구현 흐름을 따라가되, 개발 환경은 macOS와 Apple Silicon 환경에 맞게 구성합니다.
구현 이전에 흐름 파악을 먼저 진행합니다.

## Study Log

학습 과정과 시행착오는 [`DEVLOG.md`](./DEVLOG.md)에 기록합니다.

## Principle

> 완성보다 이해, 진도보다 사고, 정답보다 직접 디버깅.

