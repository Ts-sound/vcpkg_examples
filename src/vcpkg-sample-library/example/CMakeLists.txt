cmake_minimum_required(VERSION 3.10)
project(sample_app)

# Find the vcpkg-sample-library package
find_package(my_sample_lib CONFIG REQUIRED)

# Create the executable
add_executable(sample_app main.cpp)

# Link against the library using the imported target
target_link_libraries(sample_app PRIVATE my_sample_lib::my_sample_lib)
