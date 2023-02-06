# AmbiqSuiteSDK

A copy of the AmbiqSuite SDK available on GitHub. Can be used to include
AmbiqSuite as a submodule. Can be used to track issues with the SDK, however it
is not maintained by AmbiqMicro so the issues may not be resolved upstream.

# Current Version
2.4.2

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
git clone --recursive https://github.com/sparkfun/AmbiqSuiteSDK
cd AmbiqSuiteSDK
mkdir build
meson setup --prefix [custom-prefix] --cross-file ../redboard_artemis --buildtype release
meson compile
meson install
```

# Advanced Usage
All the convenient functionality that we've added to the AmbiqSuiteSDK comes
from our [SparkFun AmbiqSuite Apollo3
BSPs](https://github.com/sparkfun/SparkFun_Apollo3_AmbiqSuite_BSPs). That repo
contains more [detailed documentation for advanced
usage](https://github.com/sparkfun/SparkFun_Apollo3_AmbiqSuite_BSPs#advanced-usage).

# Repository Structure
In addition to including the [SparkFun
BSPs](https://github.com/sparkfun/SparkFun_Apollo3_AmbiqSuite_BSPs)This repo
catalogs information about the AmbiqSuite SDK. Various branches serve different
purposes:

### Branch Purposes

Pattern | Use | Addtl. info
---|---|---
master | contains the most up-to-date version of the SDK along with all patches |
mirror | mirrors latest SDK available from AmbiqMicro |
\*-archive | provides an archive of the SDK as released by AmbiqMicro at each version |
\*-patch-\*description| provides a version of the SDK patched beyond AmbiqMicro release


# Submodules
Git submodules can be used to reuse code between repositories. Some special
precautions can be necessary when working with them -- most notably the need to
clone the contents of submodules explicitly. Here's how to do that:

- If you've already cloned a repo
  - ```git submodule update --init --recursive```
- If you are about to clone the repo
  - ```git clone --recursive <project url>```

Maintainers of this repo may also need to keep submodules updated.

Here are some more documents about submodules.
- [Working with Submodules by GitHub](https://github.blog/2016-02-01-working-with-submodules/)
- [Git Submodules by gitaarik](https://gist.github.com/gitaarik/8735255)

This repo includes the following git submodules:
- [SparkFun_Apollo3_AmbiqSuite_BSPs](https://github.com/sparkfun/SparkFun_Apollo3_AmbiqSuite_BSPs) : provides board definitions and examples for SparkFun Apollo3 boards
