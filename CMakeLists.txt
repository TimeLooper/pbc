cmake_minimum_required(VERSION 3.10)

project(pbc)

# output
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)

include_directories(${CMAKE_CURRENT_LIST_DIR})

aux_source_directory(${CMAKE_CURRENT_LIST_DIR}/src LIBSRCS)

set(LIBNAME "pbc")

add_library(${LIBNAME} STATIC ${LIBSRCS})
if(WIN32)
set_source_files_properties(${LIBSRCS} PROPERTIES LANGUAGE CXX)
endif(WIN32)

### install header
install(FILES "${CMAKE_CURRENT_LIST_DIR}/pbc.h" DESTINATION "include")

### install library
install(TARGETS ${LIBNAME}
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
