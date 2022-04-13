# -*- Mode: CMake; indent-tabs-mode: nil; tab-width: 4 -*-
#
# Copyright (C) 2022 Canonical, Ltd.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; version 3.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

cmake_minimum_required(VERSION 3.2)
project(anon-shm-preload)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "" FORCE)
endif(NOT CMAKE_BUILD_TYPE)

set(ANON_SHM_PRELOAD "anon-shm-preload")
set(LIBNAME "lib${ANON_SHM_PRELOAD}")
set(LIBPATH "lib")
add_library(${ANON_SHM_PRELOAD} SHARED preload.cpp)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")

configure_file(anon-shm-preload.in anon-shm-preload @ONLY)

install(TARGETS ${ANON_SHM_PRELOAD} LIBRARY DESTINATION ${LIBPATH})
install(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/anon-shm-preload DESTINATION bin)
