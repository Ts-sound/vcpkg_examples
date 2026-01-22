# vcpkg_examples

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A collection of practical examples demonstrating how to use [vcpkg](https://github.com/microsoft/vcpkg), the C++ package manager, for building cross-platform C++ applications with CMake.

## What is vcpkg?

vcpkg is Microsoft's C++ package manager that simplifies the acquisition and installation of third-party libraries on Windows, Linux, and macOS. It provides a declarative manifest format for specifying dependencies and integrates seamlessly with CMake projects.

## Prerequisites

Before running these examples, ensure you have the following installed:

- [CMake](https://cmake.org/) (version 3.10 or higher)
- [vcpkg](https://github.com/microsoft/vcpkg)
- A C++ compiler (GCC, Clang, MSVC, etc.)
- Make or Ninja build system

### Installing vcpkg

```bash
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
./bootstrap-vcpkg.sh  # On Linux/macOS
# or bootstrap-vcpkg.bat on Windows
```

Set the `VCPKG_ROOT` environment variable to point to your vcpkg installation:

```bash
export VCPKG_ROOT=/path/to/vcpkg
export PATH=$VCPKG_ROOT:$PATH
```

## Project Structure

```
vcpkg_examples/
├── src/
│   ├── helloworld/           # Basic example using fmt library
│   │   ├── CMakeLists.txt
│   │   ├── helloworld.cpp
│   │   ├── vcpkg.json        # Manifest file
│   │   └── vcpkg-configuration.json
│   └── vcpkg-sample-library/ # Custom library example
│       ├── vcpkg.json
│       ├── portfile.cmake
│       └── usage
├── LICENSE
├── README.md
└── .gitignore
```

## Examples

### Hello World

A simple C++ application that demonstrates basic vcpkg usage with the [fmt](https://github.com/fmtlib/fmt) library for formatted output.

#### Building and Running

```bash
cd src/helloworld

# Install dependencies (installed to local vcpkg_installed directory)
vcpkg install

# Build the project (general method, not using CMakePresets.json)
mkdir build && cd build
cmake .. \
  -DCMAKE_BUILD_TYPE=Debug \
  -DVCPKG_INSTALLED_DIR=./vcpkg_installed \
  -DCMAKE_TOOLCHAIN_FILE=$VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake
make

# Run the application
./HelloWorld
```

**Expected output:**

```
Hello World!
```

### Cross-Compilation Example

This example demonstrates how to cross-compile the Hello World application for ARM64 Linux using vcpkg.

#### Prerequisites for Cross-Compilation

- ARM64 cross-compiler toolchain
- Set the toolchain path in your PATH

```bash
# Export the cross-compiler bin path
export PATH=$PATH:/opt/tong/toolchain/gcc-linaro-7.5.0-2019.12-x86_64_aarch64-linux-gnu/bin

cd src/helloworld

# Install dependencies for ARM64 Linux triplet
vcpkg install --triplet arm64-linux

# Build for ARM64
mkdir build_arm64 && cd build_arm64
cmake .. \
  -DCMAKE_BUILD_TYPE=Debug \
  -DVCPKG_INSTALLED_DIR=./vcpkg_installed \
  -DCMAKE_TOOLCHAIN_FILE=$VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake \
  -DVCPKG_TARGET_TRIPLET=arm64-linux \
  -DCMAKE_C_COMPILER=aarch64-linux-gnu-gcc \
  -DCMAKE_CXX_COMPILER=aarch64-linux-gnu-g++ \
  -DCMAKE_SYSTEM_NAME=Linux \
  -DCMAKE_SYSTEM_PROCESSOR=aarch64
make

# Verify the binary architecture
file HelloWorld
```

**Expected output:**

```
HelloWorld: ELF 64-bit LSB executable, ARM aarch64, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux-aarch64.so.1, for GNU/Linux 3.7.0, BuildID[sha1]=..., with debug_info, not stripped
```

### Custom Library Example

The `vcpkg-sample-library` directory contains an example of creating a custom vcpkg port for a library. This demonstrates how to package and distribute your own C++ libraries using vcpkg.

See the `usage` file and `portfile.cmake` for details on creating custom ports.

## Configuration Files

### vcpkg.json

The manifest file that declares project dependencies:

```json
{
  "dependencies": [
    "fmt"
  ]
}
```

### vcpkg-configuration.json

Optional configuration file for advanced vcpkg settings (registries, overlays, etc.).

## Troubleshooting

### Common Issues

1. **CMake cannot find vcpkg toolchain**
   - Ensure `VCPKG_ROOT` environment variable is set correctly
   - Verify the path to `vcpkg.cmake` in `CMAKE_TOOLCHAIN_FILE`

2. **Dependencies not found**
   - Run `vcpkg install` in the project directory
   - Check that the triplet matches your target platform

3. **Cross-compilation fails**
   - Verify cross-compiler is in PATH
   - Ensure correct triplet is specified (`--triplet`)

### Getting Help

- [vcpkg Documentation](https://vcpkg.readthedocs.io/)
- [vcpkg GitHub Issues](https://github.com/microsoft/vcpkg/issues)
- [CMake Documentation](https://cmake.org/documentation/)

## Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
