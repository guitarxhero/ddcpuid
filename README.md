# ddcpuid, CPUID tool

ddcpuid is a x86 processor information tool. Currently supports Intel and AMD
processors.

- Can be used as a stand-alone tool or as a library.
- BetterC compatible.
- DUB compatible.
- Does not rely on either the C runtime nor the D runtime.
- Surpasses CPU-Z, [Intel's Go CPUID](https://github.com/intel-go/cpuid/) module, and Druntime's `core.cpuid` module.
- _Currently featuring 240 CPUID bits documented and counting!_

The latest version of the technical ddcpuid manual is available here:
[dd86k.space](https://dd86k.space/docs/ddcpuid-manual.pdf) (PDF).

Both the manual and tool is meant to be used together to better understand x86.

# Compiling

The best way to compile ddcpuid is using DUB.

Compilers supported:
- DMD >= 2.068.0 (best supported)
- LDC >= 0.17.1 (best optimizations, but see [LDC Issues](#ldc-issues))
- GDC >= 6.0.0 (experimental, see [GDC Issues](#gdc-issues))

## DUB

Using dub(1) is rather straightforward.

To learn how to use DUB, visit [this page](https://dub.pm/commandline.html).

## Makefile

The Makefile relies on GNU Make (gmake/gnumake).

Available variables:
- `DC`: D compiler, defaults to `dmd`
- `PREFIX`: installation path prefix, defaults to `/usr/local`

Available actions:
- debug (default)
- release
- install
- uninstall

Examples:
- `make`: Produce a debug build
- `make release DC=ldc`: Produce a release build with LDC

## Manually

Since ddcpuid only consists of two files, both being in the `src` folder, it's
still easy to perform manual compilations.

## GDC Issues

### Optimizations

Compiling above O0 will yield invalid results, and that's because of my
incapability to understand the complex extended GCC inline assembler
format. I very much dislike it.

## LDC Issues

### Legacy stdio Definitions

On Windows, LDC versions 1.13 and 1.14 do not include
`legacy_stdio_definitions.lib`, making it impossible to compile the project
using `-betterC`.