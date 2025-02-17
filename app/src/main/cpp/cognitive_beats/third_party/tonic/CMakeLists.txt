cmake_minimum_required(VERSION 2.6)

#set project name
set(PRJ_NAME tonic)
#indicate type of the project as executable, otherwise it is a library
#set(PRJ_TYPE_EXECUTABLE 1)
#allways build libarary (with object files)
set(PRJ_BUILD_LIBRARY 1)
#main file name - used to filter this with object files
#set(PRJ_MAIN_FILE "main.c")

#libraries to link
set(LINK_LIBS "")
#define cflags
set(CFLAGS "")
#define header include directories as list
set(INCLUDE_DIR)


# Compiler Specific 
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  # using Clang
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  # enable sse
  add_definitions("-msse2")
  # using GNU
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Intel")
  # using Intel C++
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
  # using Visual Studio C++
endif()

message("using compiler '${CMAKE_CXX_COMPILER_ID}' ('${CMAKE_CXX_COMPILER}')")

# Generator Specific
# Compiler Specific 
if ("${CMAKE_GENERATOR}" STREQUAL "Xcode")
  # fixes an issues in the Xcode generator which produces endless warnings
  add_definitions("-Wno-unused")
elseif ("${CMAKE_GENERATOR}" STREQUAL "MinGW Makefiles")
  # MinGW needs to explicitely enable sse
  add_definitions("-msse2")
  # disable xcode pragma warning
  add_definitions("-Wno-unknown-pragmas")
  # disable unused XYZ warnings
  add_definitions("-Wno-unused")
endif()

message("using generator '${CMAKE_GENERATOR}'")

# Including the required Frameworks
IF(APPLE)
   INCLUDE_DIRECTORIES ( /System/Library/Frameworks )
   SET(EXTRA_LIBS 
	   	"-framework CoreFoundation" 
	   	"-framework CoreAudio" 
	   	"-framework Accelerate" 
	   	"-framework AudioToolbox")
   message("using frameworks ${EXTRA_LIBS}")
ENDIF (APPLE)

project(${PRJ_NAME})

add_subdirectory(src)
add_subdirectory(tests)
#add_subdirectory(examples)

#set enable testing
enable_testing()