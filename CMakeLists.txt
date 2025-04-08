cmake_minimum_required(VERSION 3.15)

set(CMAKE_TOOLCHAIN_FILE "c:/vcpkg/scripts/buildsystems/vcpkg.cmake"
    CACHE STRING "Vcpkg toolchain file")
# Project name
project(VCPKG_Raylib_Project)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
# set(CMAKE_PREFIX_PATH "C:/vcpkg/installed/x64-windows")

# Find raylib package
find_package(raylib CONFIG REQUIRED)

# Add executable
add_executable(main main.cpp)

# Link raylib to the project
target_link_libraries(main PRIVATE raylib)
