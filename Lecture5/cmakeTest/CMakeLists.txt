# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.10)

# 1. Project Definition
# Define the project name (it's good practice to match the executable name or a library/module)
project(myROOTCommand_Project CXX)

# 2. Set C++ Standard
# Equivalent to: cc=g++ -std=c++17 ...
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 3. Find ROOT
# This module will look for ROOT libraries and set necessary variables
# Equivalent to: `root-config --cflags` and `root-config --libs`
find_package(ROOT REQUIRED)

# 4. Add Executable
# Define the target executable and its source file
# Equivalent to: OBJECTS := myROOTCommand.o
add_executable(${PROJECT_NAME} myROOTCommand.cpp)

# 5. Link Libraries and Set Compile/Link Flags
# This section connects the executable to ROOT's settings and libraries
#
# Equivalent to the compiler flags from your Makefile:
# - Wall, -g, -I $(shell root-config --cflags)
#
# Equivalent to the linker line from your Makefile:
# g++ -Wl,-rpath,${ROOTSYS}/lib -g -Wall -o $@ $^ `root-config --libs` -lvectorDict

# Include directories (for headers)
target_include_directories(${PROJECT_NAME} PRIVATE ${ROOT_INCLUDE_DIRS})

# Libraries to link (for the executable)
# Note: ROOT_LIBRARIES contains the result of `root-config --libs`, including the RPATH setup.
# The 'vectorDict' library is added explicitly.
target_link_libraries(${PROJECT_NAME} PRIVATE ${ROOT_LIBRARIES})

# Optional: Add compiler flags like -Wall and -g (debug)
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -g)

