# vcpkg-sample-library

A sample C++ library demonstrating how to create custom vcpkg ports. This library serves as a practical example for packaging libraries with vcpkg.

---

## Overview

vcpkg-sample-library is a minimal C++ library that provides a simple "Hello World" function. It demonstrates the complete workflow of creating, packaging, and distributing a C++ library through vcpkg.

---

## Features

- Simple C++ library example
- Depends on `fmt` for string formatting
- Configured with CMake
- Supports static library linkage
- Provides CMake targets for easy integration

---

## Project Structure

```bash
vcpkg-sample-library/
├── vcpkg.json          # Port manifest
├── portfile.cmake      # Build instructions
├── usage               # Usage documentation
└── README.md           # This file
```

---

## File Descriptions

### vcpkg.json

Defines the port metadata and dependencies:

```json
{
  "name": "vcpkg-sample-library",
  "version": "1.0.2",
  "description": "A sample C++ library designed to serve as a foundational example for a tutorial on packaging libraries with vcpkg.",
  "homepage": "https://github.com/MicrosoftDocs/vcpkg-docs/tree/cmake-sample-lib",
  "license": "MIT",
  "dependencies": [
    "fmt",
    {
      "name": "vcpkg-cmake",
      "host": true
    },
    {
      "name": "vcpkg-cmake-config",
      "host": true
    }
  ]
}
```

### portfile.cmake

Contains the build and installation logic:

- Downloads the library source from GitHub
- Configures with CMake
- Installs the library
- Sets up CMake config files
- Removes debug headers
- Installs copyright and usage information

---

## Usage

### Installing the Library

Add to your `vcpkg.json` manifest:

```json
{
  "dependencies": [
    "vcpkg-sample-library"
  ]
}
```

Then run:

```bash
vcpkg install
```

### Using in Your Project

Add to your `CMakeLists.txt`:

```cmake
find_package(my_sample_lib CONFIG REQUIRED)
target_link_libraries(main PRIVATE my_sample_lib::my_sample_lib)
```

### Example Code

```cpp
#include <my_sample_lib/hello.hpp>

int main() {
    my_sample_lib::say_hello();
    return 0;
}
```

---

## Port Configuration Details

### Build Process

1. Download source from GitHub (MicrosoftDocs/vcpkg-docs)
2. Configure with CMake
3. Install library files
4. Generate and install CMake config files
5. Clean up debug headers
6. Install usage documentation and license

---

## Creating Your Own Port

Based on this example, to create your own vcpkg port:

1. Create a new directory in vcpkg/ports/
2. Add a `portfile.cmake` with build instructions
3. Add a `vcpkg.json` with metadata
4. Add a `usage` file with integration instructions
5. Optionally add patches for source modifications

---

## License

This library is licensed under the MIT License.

---

## References

- [vcpkg Documentation](https://vcpkg.readthedocs.io/)
- [Creating a Port](https://vcpkg.readthedocs.io/en/latest/examples/packaging-zipfiles-and-installing-dlls-dlls-with-golang/)
- [portfile.cmake Reference](https://learn.microsoft.com/en-us/vcpkg/users/portfile-functions)
