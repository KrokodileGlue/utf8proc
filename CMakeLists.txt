cmake_minimum_required (VERSION 2.8.12)

include (utils.cmake)

disallow_intree_builds()

project (utf8proc C)

# This is the ABI version number, which may differ from the
# API version number (defined in utf8proc.h).
# Be sure to also update these in Makefile and MANIFEST!
set(SO_MAJOR 2)
set(SO_MINOR 1)
set(SO_PATCH 1)

if (NOT MSVC)
  set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O2 -std=c99 -pedantic -Wall")
endif ()

add_library (utf8proc
  utf8proc.c
  utf8proc.h
)

target_compile_definitions(utf8proc PRIVATE "UTF8PROC_EXPORTS")

set_target_properties (utf8proc PROPERTIES
  POSITION_INDEPENDENT_CODE ON
  VERSION "${SO_MAJOR}.${SO_MINOR}.${SO_PATCH}"
  SOVERSION ${SO_MAJOR}
)
