#*********************************************************************
# Copyright (C) Dietrich Epp, 2012. All rights reserved.
# Copyright (C) Anton Kovalev, 2021-2022. All rights reserved.
# libfresample
# BSD-2 License
#****************************************************************/

cmake_minimum_required(VERSION 3.8)
project(fresample C CXX)

set(BUILD_STAFF 1)
set(CMAKE_INCLUDE_CURRENT_DIRS ON)
set(FRESAMPLE_STATIC ON)

file(GLOB FRESAMPLE_SRC
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.hpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h"
)

if (CMAKE_CXX_COMPILER_ID STREQUAL "Clang" AND WIN32)
	set(FRESAMPLE_USE_CLANG_CL ON)
else()
	set(FRESAMPLE_USE_CLANG_CL OFF)
endif()

if (FRESAMPLE_STATIC)
    add_library(fresample STATIC ${FRESAMPLE_SRC})
else()
    add_library(fresample MODULE ${FRESAMPLE_SRC})
endif()

target_include_directories(fresample PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_compile_definitions(fresample PRIVATE CLANGCL_COMPILER)