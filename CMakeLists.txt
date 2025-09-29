#########################
# Project configuration #
#########################

cmake_minimum_required(VERSION 3.15)
project(VCPKG_Raylib_Project)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)  # MSVC, works with ninja but not with MSBuild

set(SOURCE_FILES src/main.cpp)
set(PROJECT_TARGET main)
#########################
#   Target Declaration  #
#########################

# Add executable
add_executable(${PROJECT_TARGET} ${SOURCE_FILES})

#############################
#   Target Configuration    #
#############################

# Find packages
find_package(raylib CONFIG REQUIRED)
find_package(glfw3 CONFIG REQUIRED)

# Link corresponding packages and default libraries
target_link_libraries(${PROJECT_TARGET} PRIVATE raylib glfw winmm)