#
# Project Ketchup libraries - CMake build file
#

# Require CMake version 2.5 or above
cmake_minimum_required (VERSION 2.6)

# The name of this project
project (CroqueNote)

# Setup version (TODO)

# Setup platform specific defines

if(WIN32)
add_definitions(-DWIN32 -DX86 -DUNICODE -D_UNICODE)
endif(WIN32)

if(APPLE)

add_definitions(-DMACOSX -DX86)

SET (SDKVER "10.5")
SET (SDKROOT "/Developer/SDKs/MacOSX10.5.sdk")
SET (CMAKE_OSX_SYSROOT "${SDKROOT}")
SET (CMAKE_OSX_ARCHITECTURES "i386")

endif(APPLE)

if(UNIX AND NOT APPLE)
add_definitions(-DLINUX -DX86)
endif(UNIX AND NOT APPLE)

# Setup static CRT linking for MSVC
# so that we don't depend on CRT DLLs
if(MSVC)
# We statically link to reduce dependancies
foreach(flag_var CMAKE_CXX_FLAGS CMAKE_CXX_FLAGS_DEBUG CMAKE_CXX_FLAGS_RELEASE CMAKE_CXX_FLAGS_MINSIZEREL CMAKE_CXX_FLAGS_RELWITHDEBINFO)
    if(${flag_var} MATCHES "/MD")
        string(REGEX REPLACE "/MD" "/MT" ${flag_var} "${${flag_var}}")
    endif(${flag_var} MATCHES "/MD")
    if(${flag_var} MATCHES "/MDd")
        string(REGEX REPLACE "/MDd" "/MTd" ${flag_var} "${${flag_var}}")
    endif(${flag_var} MATCHES "/MDd")
endforeach(flag_var)
endif(MSVC)

# Setup output directories for binary products
SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR})
SET(LIBRARY_OUTPUT_PATH    ${PROJECT_BINARY_DIR})

# Add our directories
add_subdirectory (src) 