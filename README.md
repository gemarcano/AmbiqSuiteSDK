# AmbiqSuiteSDK for the Apollo 3

This is a fork of the AmbiqSuiteSDK made available by Sparkfun, with support
for their RedBoard and Artemis Apollo3 module. This fork adds support for
building the SDK using meson.

# Current SDK Version
3.0.0 (possibly the last version supporting the Apollo3 MCUs)

# Getting Started

First make sure that the necessary tools are available at your command line.
They are:
- Git
  - ```git```
- ARM GCC
  - ```arm-none-eabi-xxx``` (preferably newer than GCC 10)
- Python3
  - ```python3```
- Meson
- pkgconf

The Meson build system uses cross files to describe cross compilation
environments. This project includes a cross file that uses arm-none-eabi GCC
tools to build the library. In order to install the statically-built library,
meson must be provided a prefix directory where the library will be installed,
along with pkgconf support files.

Applications using this library must provide a cross file with a `[constant]`
entry for the `prefix` variable, used by Meson's `pkgconf` support to determine
where to find the pkgconf information.

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
