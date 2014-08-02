# Copyright (C) 2007-2012 LuaDist.
# Created by Peter Kapec
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.

PROJECT(ogg C)
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
include ( cmake/dist.cmake )

include ( CheckIncludeFile )

# Specify library include directories
	include_directories("${PROJECT_SOURCE_DIR}/include")
	include_directories("${PROJECT_SOURCE_DIR}/include/ogg")

set(SIZE16 int16_t)
set(USIZE16 uint16_t)
set(SIZE32 int32_t)
set(USIZE32 uint32_t)
set(SIZE64 int64_t)
set(USIZE64 uint64_t)
configure_file (
  "${PROJECT_SOURCE_DIR}/include/ogg/config_types.h.in"
  "${PROJECT_BINARY_DIR}/config_types.h"
  )
# First, compiler definitions for building the library
	ADD_DEFINITIONS(-D_USRDLL)
	ADD_DEFINITIONS(-DLIBOGG_EXPORTS)

set(BASE_SRCS
    src/bitwise.c
    src/framing.c)

IF (${BUILD_SHARED_LIBS})
	ADD_LIBRARY(ogg SHARED ${BASE_SRCS} )
ELSE()
    ADD_LIBRARY(ogg STATIC ${BASE_SRCS} )
ENDIF()

# Install Ogg Library
	install_library(ogg)

# Install Ogg Headers
	install_header(include/)
	install_header("${PROJECT_BINARY_DIR}/config_types.h" INTO "ogg/")




