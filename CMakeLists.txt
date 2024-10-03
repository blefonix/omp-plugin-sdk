# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.12)

# Define your project and specify the language
project(samp-plugin-sdk)

# Add the include directories
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/amx)

# Create a library from the sources
add_library(samp-plugin-sdk SHARED
  src/amxplugin.cpp
)

target_include_directories(${PROJECT_NAME} PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>)

include(CheckIncludeFile)

check_include_file(alloca.h HAVE_ALLOCA_H)
if(HAVE_ALLOCA_H)
  add_definitions(-DHAVE_ALLOCA_H)
endif()
check_include_file(inttypes.h HAVE_INTTYPES_H)
if(HAVE_INTTYPES_H)
  add_definitions(-DHAVE_INTTYPES_H)
endif()
check_include_file(malloc.h HAVE_MALLOC_H)
if(HAVE_MALLOC_H)
  add_definitions(-DHAVE_MALLOC_H)
endif()
check_include_file(stdint.h HAVE_STDINT_H)
if(HAVE_STDINT_H)
  add_definitions(-DHAVE_STDINT_H)
endif()


# Install headers
include(GNUInstallDirs)
install(TARGETS ${PROJECT_NAME}
    ARCHIVE  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY  DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME  DESTINATION ${CMAKE_INSTALL_BINDIR})
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})