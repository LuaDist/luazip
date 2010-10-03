# Copyright (C) 2007-2009 LuaDist.
# Created by Peter Kapec
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.

PROJECT(luazip C)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
INCLUDE(dist.cmake)

SET(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_MODULE_PATH})

# Zlib library needed
FIND_PACKAGE(ZLIB REQUIRED)
INCLUDE_DIRECTORIES(${ZLIB_INCLUDE_DIR})

# zziplib library needed
FIND_PACKAGE(zziplib REQUIRED)
INCLUDE_DIRECTORIES(${ZZIPLIB_INCLUDE_DIRS})

# luazip modules
INCLUDE_DIRECTORIES(src)

ADD_LUA_MODULE(zip src/luazip.c src/luazip.def)
TARGET_LINK_LIBRARIES(zip ${ZZIPLIB_LIBRARIES} ${ZLIB_LIBRARIES})

#~2DO: run test_zip.lua with working directory tests.

# Install
INSTALL (TARGETS zip DESTINATION ${INSTALL_CMOD})
INSTALL(FILES README DESTINATION ${INSTALL_DATA})
INSTALL(DIRECTORY doc/ DESTINATION ${INSTALL_DOC})
INSTALL(DIRECTORY tests/ DESTINATION ${INSTALL_TEST})
