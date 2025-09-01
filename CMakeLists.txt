cmake_minimum_required(VERSION 3.10)
cmake_policy(SET CMP0054 NEW)

project(pbc)

# default release
if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Set build type to Debug or Release (default Release)" FORCE)
endif ()

string(TOLOWER "${CMAKE_BUILD_TYPE}" CMAKE_BUILD_TYPE_LOWER)

set(CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING "Limited configurations" FORCE)

# output
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)

include_directories(${CMAKE_CURRENT_LIST_DIR})

aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src LIBSRCS)

set(LIBNAME "pbc")

add_library(${LIBNAME} STATIC ${LIBSRCS})

### install header
install(FILES "${CMAKE_CURRENT_LIST_DIR}/pbc.h" DESTINATION "include")

### install library
install(TARGETS ${LIBNAME}
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
