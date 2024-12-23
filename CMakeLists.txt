# Copyright (C) 2015 Christopher Gilbert.
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

#
# Project Properties
#
CMAKE_MINIMUM_REQUIRED (VERSION 3.23.0)
PROJECT (aho_corasick)
SET(AHO_CORASICK_TEST OFF)

#
# Debugging Options
#
SET (CMAKE_VERBOSE_MAKEFILE 0) # Use 1 for debugging, 0 for release

#
# Project Output Paths
#
SET (MAINFOLDER ${PROJECT_SOURCE_DIR})

#
# Project Search Paths
#
LIST (APPEND CMAKE_PREFIX_PATH "${MAINFOLDER}")
SET (CMAKE_MODULE_PATH "${MAINFOLDER}/cmake")
INCLUDE_DIRECTORIES ("${MAINFOLDER}/src")

#
# Enable C++23
#
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Unicode support
find_package(ICU REQUIRED COMPONENTS uc)
include_directories(${ICU_INCLUDE_DIR})
if (WIN32)
  SET(ICU_UC_LIBRARY "$ENV{ICU_ROOT}/lib64/icuuc.lib")
  SET(ICU_LIBRARIES "${ICU_UC_LIBRARY}")
endif()

#
# Recurse source sub-directories
#
if (AHO_CORASICK_TEST)
  ENABLE_TESTING (true)
endif()
ADD_SUBDIRECTORY (src)
if (AHO_CORASICK_TEST)
  ADD_SUBDIRECTORY (test)
endif()
