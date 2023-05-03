# AmbiqSuiteSDK for the Apollo 3

This is a fork of the AmbiqSuiteSDK made available by Sparkfun, with support
for their RedBoard and Artemis Apollo3 module. This fork adds support for
building the SDK using meson.

## Current SDK Version
3.0.0 (possibly the last version supporting the Apollo3 MCUs)

## Getting Started

First make sure that the necessary tools are available at your command line.
They are:
 - `git`
 - `arm-none-eabi-xxx` (preferably newer than GCC 10)
 - `python3`
 - `meson`
 - `pkgconf`

The Meson build system uses cross files to describe cross compilation
environments. This project includes a cross file that uses arm-none-eabi GCC
tools to build the library. In order to install the statically-built library,
meson must be provided a prefix directory where the library will be installed,
along with pkgconf support files.

Applications using this library must provide a cross file with a `[constant]`
entry for the `prefix` variable, used by Meson's `pkgconf` support to determine
where to find the pkgconf information.

## Building the Library

The following is an example on how to install the library:

```
git clone --recursive https://github.com/gemarcano/AmbiqSuiteSDK
cd AmbiqSuiteSDK
git submodule update --init --recursive
mkdir build
cd build
meson setup --prefix [custom-prefix] --cross-file ../artemis --buildtype release
meson install
```

The meson build system builds a library and creates an associated pkgconfig
configuration file for all of the Sparkfun Artemis boards in the `boards_sfe`
directory. Currently, these libraries are:
 - `libambiq_a_tp.a` for the Artemis Thing Plus
 - `libambiq_micromod.a` for the Artemis Micromod
 - `libambiq_rba.a` for the RedBoard Artemis
 - `libambiq_rba_nano.a` for the RedBoard Artemis Nano
 - `libambiq_dk.a` for the Artemis Development Kit
 - `libambiq_module.a` for the Artemis Module
 - `libambiq_rba_atp.a` for the RedBoard Artemis All-the-Pins
