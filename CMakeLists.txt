# Philipp Neufeld, 2023

cmake_minimum_required (VERSION 3.17)

# don't allow build in the source directory
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
   message(FATAL_ERROR "You don't want to configure in the source directory! Please use cmake [<options>] -S <path-to-source> -B <path-to-build>")
endif()

# define project
project ("QtTest" VERSION 1.0)

# include directories
add_executable("QtTest" "main.cpp" )

# require C++17 for library and all children using it
target_compile_features("QtTest" PUBLIC cxx_std_17)

# set include directory as interface
set(INCLUDE_DIR "${CMAKE_SOURCE_DIR}")
target_include_directories("QtTest" INTERFACE "${INCLUDE_DIR}")

# find Qt5
find_package(Qt5 COMPONENTS Core Widgets REQUIRED)
target_link_libraries("QtTest" PUBLIC Qt5::Core)
target_link_libraries("QtTest" PUBLIC Qt5::Widgets)

