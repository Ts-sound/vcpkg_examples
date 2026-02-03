# vcpkg-sample-library Usage Example

This example demonstrates how to use the `vcpkg-sample-library` in a C++ project.

---

## Project Structure

```bash
example/
├── CMakeLists.txt      # Build configuration
├── main.cpp            # Sample application
├── vcpkg.json          # Dependencies manifest
└── README.md           # This file
```

---

## Building the Example

### Prerequisites

1. vcpkg installed and `VCPKG_ROOT` environment variable set
2. CMake 3.10 or higher
3. C++11 compatible compiler

### Step 1: Install Dependencies

```bash
cd src/vcpkg-sample-library/example
vcpkg install
```

This will install `vcpkg-sample-library` and its dependencies (fmt) to the local `vcpkg_installed` directory.

### Step 2: Configure CMake

```bash
mkdir build && cd build
cmake .. \
  -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_TOOLCHAIN_FILE=$VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake
```

### Step 3: Build

```bash
cmake --build .
```

### Step 4: Run

```bash
./sample_app
```

**Expected Output:**

```bash
Demonstrating vcpkg-sample-library usage:
Hello, helloworld!
```

---

## Code Explanation

### CMakeLists.txt

```cmake
# Find the vcpkg-sample-library package
find_package(my_sample_lib CONFIG REQUIRED)

# Create the executable
add_executable(sample_app main.cpp)

# Link against the library using the imported target
target_link_libraries(sample_app PRIVATE my_sample_lib::my_sample_lib)
```

Key points:

- `find_package()` locates the library using CMake config files
- `my_sample_lib::my_sample_lib` is the imported target provided by the library
- Linking with `PRIVATE` specifies that the library is only needed for building the target

---

## Using in Your Own Projects

### 1. Add Dependency to vcpkg.json

```json
{
  "name": "your-project",
  "version": "1.0.0",
  "dependencies": [
    "vcpkg-sample-library"
  ]
}
```

### 2. Find and Link in CMakeLists.txt

```cmake
find_package(my_sample_lib CONFIG REQUIRED)
target_link_libraries(your_target PRIVATE my_sample_lib::my_sample_lib)
```

### 3. Include Headers

```cpp
#include <my_sample_lib.h>
```

---

## Troubleshooting

### Package not found

**Error:** `Could not find package my_sample_lib`

**Solution:** Run `vcpkg install vcpkg-sample-library` or add it to your `vcpkg.json` and run `vcpkg install`

### fmt not found

**Error:** `Could not find fmt`

**Solution:** `vcpkg-sample-library` depends on `fmt`. Running `vcpkg install vcpkg-sample-library` will install the dependency automatically.

### CMake toolchain not found

**Error:** CMake cannot find vcpkg.cmake

**Solution:** Ensure `VCPKG_ROOT` is set and the path is correct:

```bash
export VCPKG_ROOT=/path/to/vcpkg
cmake .. -DCMAKE_TOOLCHAIN_FILE=$VCPKG_ROOT/scripts/buildsystems/vcpkg.cmake
```

---

## Best Practices

1. **Use Imported Targets**: Always link with `my_sample_lib::my_sample_lib` instead of specifying library paths manually

2. **Modern CMake**: Prefer target-based properties over legacy variables

3. **Dependency Specifications**: Use `PUBLIC`, `PRIVATE`, or `INTERFACE` appropriately:
   - `PUBLIC`: Dependency is needed by both the target and consumers
   - `PRIVATE`: Dependency is only needed by the target
   - `INTERFACE`: Dependency is only needed by consumers

4. **Version Pinning**: Consider pinning versions in `vcpkg.json` for reproducible builds:

```json
{
  "dependencies": [
    {
      "name": "vcpkg-sample-library",
      "version>=": "1.0.0"
    }
  ]
}
