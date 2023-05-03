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

## Fetching the Library

```
git clone --recursive https://github.com/gemarcano/AmbiqSuiteSDK
```

## Building the Library

From the repository directory:
```
mkdir build
cd build
meson setup --prefix [custom-install-prefix] --cross-file ../artemis --buildtype release
meson compile
```

A custom install prefix is strongly encouraged, to prevent installing the
library into `/usr/local` or other host folders.

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

## Installing

From the `build` directory:
```
meson install
```

This will install the library in the `[custom-install-prefix]` provided during
setup.

One additional recommended step is to copy the `artemis` cross-file from the
root of the repository to `$HOME/.local/share/meson/cross/`. This will make it
so that the cross-file can be used from any meson project merely by adding
`--cross-file artemis`.

## How to use

### Meson

The recommended approach is to create a meson project and use the `--prefix`
and updating the `pkg_config_libdir` to point to a cross-file to the prefix
where this library was installed. If using the `artemis` cross-file from this
repository, it exposes a variable in the `[constants]` cross-file section that
can be overwritten in a second cross-file. This variable is aptly named
`prefix`. This secondary cross-file might look like:

```
[constants]
prefix = '[install-prefix-absolute-path]'
```

Replace `[install-prefix-absolute-path]` with the absolute path to the prefix
specified when setting up the AmbiqSuiteSDK build.

### Manually

More generally, this project generates pkgconfig files that can be used to
figure out what compilation and linking flags are necessary. These files are
installed in the `[prefix]/lib/pkgconfig/libambiq*.pc` files.
