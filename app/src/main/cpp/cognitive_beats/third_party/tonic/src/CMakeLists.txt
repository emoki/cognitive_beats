#include directories helps to include header files
include_directories(".")
include_directories("Tonic")
include_directories(${INCLUDE_DIR})

#get the source filenames to compile
file(GLOB_RECURSE SOURCES Tonic/*.cpp Tonic/*.h)

add_library(${PRJ_NAME} ${SOURCES})