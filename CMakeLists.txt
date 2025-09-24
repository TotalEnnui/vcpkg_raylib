#########################
# Project configuration #
#########################

cmake_minimum_required(VERSION 3.15)
project(VCPKG_Raylib_Project)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#########################
#   Target Declaration  #
#########################

# Add executable
add_executable(main main.cpp)

#############################
#   Target Configuration    #
#############################

# Find raylib package
find_package(raylib CONFIG REQUIRED)

# Link raylib to the project
target_link_libraries(main PRIVATE raylib)