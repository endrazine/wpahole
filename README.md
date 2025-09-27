# wpahole: Extended Pahole with JSON Output

[![License](https://img.shields.io/badge/license-GPL--2.0-blue.svg)](https://github.com/endrazine/wpahole/blob/master/COPYING)

## Overview

wpahole is a forked and extended version of the original **pahole** tool from the **dwarves** project. Pahole is a utility for analyzing and pretty-printing DWARF debug information in ELF files, commonly used for tasks like BTF (BPF Type Format) encoding and struct layout inspection.

This fork adds support for **JSON-formatted output**, making it compatible with the **Witchcraft Shell (WSH)** from the [Witchcraft Compiler Collection (WCC)](https://github.com/endrazine/wcc). The JSON output allows seamless integration with WSH for scripting and automation in binary analysis workflows.

Key features:
- All original pahole functionalities.
- New `--json` option (or equivalent) for outputting results in JSON format.
- Builds an additional binary `wpahole` alongside `pahole` for easy distinction.

This project is based on the upstream dwarves/pahole repository from `git://git.kernel.org/pub/scm/devel/pahole/pahole.git`.

## Purpose

The primary extension is to enable JSON output, which is particularly useful for:
- Integrating with tools like WSH in WCC for programmatic binary introspection.
- Parsing structured data in scripts or pipelines.
- Enhancing compatibility with modern tooling that expects machine-readable formats.

For more on WCC and WSH, see the [WCC README](https://github.com/endrazine/wcc).

## Installation Requirements

wpahole requires the following dependencies (similar to upstream dwarves):
- CMake (version 3.5 or higher)
- libdw (from elfutils)
- zlib
- libbpf (embedded by default, or via pkg-config)
- argp and obstack (often in libc)
- Git (for submodule management)

On Ubuntu/Debian, install with:
```bash
sudo apt-get install -y cmake libdw-dev zlib1g-dev libelf-dev pkg-config git
```

If using the embedded libbpf, no additional packages are needed beyond the basics.

## Building and Installing

### Fetching the Code

Clone the repository:
```bash
git clone https://github.com/endrazine/wpahole.git
cd wpahole
```

### Initializing Git Submodules

Initialize and update submodules (for libbpf):
```bash
git submodule init
git submodule update
```

### Building

Create a build directory and run CMake:
```bash
mkdir build
cd build
cmake ..
make
```

This will build all tools, including `pahole` and the new `wpahole` (a copy of `pahole` for branding).

### Installing

Install system-wide (may require sudo):
```bash
sudo make install
```

By default, binaries are installed to `/usr/local/bin`, libraries to `/usr/local/lib`, etc. Customize with `-DCMAKE_INSTALL_PREFIX=/path` during CMake.

## Usage

wpahole retains all upstream pahole options. Run `wpahole --help` or `man pahole` for full details.

### Basic Example
Pretty-print struct layouts from an ELF file:
```bash
wpahole -C struct_name /path/to/elf/file
```

### New JSON Output
Use the extended JSON feature (assuming implementation via a new flag; adjust based on your modifications):
```bash
wpahole -W /path/to/elf/file > output.json
```

This outputs DWARF information in JSON format, suitable for parsing in WSH scripts or other tools.

Refer to the [WCC documentation](https://github.com/endrazine/wcc/wiki) for WSH scripting examples.

## Modifications from Upstream

- Added CMake rules to build and install `wpahole` as a copy of `pahole`.
- Implemented JSON output support (details in source diffs; see commits).
- Maintained compatibility with upstream; pull updates via `git fetch upstream`.

To contribute back or sync with upstream, fork from the original kernel.org repo and submit patches.

## License

wpahole is licensed under the GNU General Public License v2 (GPL-2.0). See [COPYING](COPYING) for details.

This fork respects the upstream license. For the original dwarves project license, refer to the kernel.org repository.

## Links

- Upstream: [git://git.kernel.org/pub/scm/devel/pahole/pahole.git](git://git.kernel.org/pub/scm/devel/pahole/pahole.git)
- Related Project: [Witchcraft Compiler Collection (WCC)](https://github.com/endrazine/wcc)
- Issues: Report bugs or feature requests [here](https://github.com/endrazine/wpahole/issues)

## About

Extended pahole with JSON output for WCC/WSH compatibility.

© 2025 Jonathan Brossard
