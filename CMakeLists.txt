# Copyright 2018, akashche at redhat.com
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required ( VERSION 2.8.12 )
project ( freetype C )

OPTION ( CMAKE_INCLUDE_DIRECTORIES_BEFORE "Prefer local libs over system ones" ON )

set ( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )
set ( CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )
set ( CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )
set ( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )
set ( CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )
set ( CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )    
set ( CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )
set ( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR} CACHE INTERNAL "" )
set ( CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR} CACHE INTERNAL "" ) 

set ( CMAKE_C_FLAGS "/D _CRT_SECURE_NO_WARNINGS /D WIN32_LEAN_AND_MEAN" CACHE INTERNAL "" )
set ( CMAKE_C_FLAGS_DEBUG "/D _DEBUG /MDd /Zi /Ob0 /Od /RTC1" CACHE INTERNAL "" )
set ( CMAKE_C_FLAGS_RELEASE "/D NDEBUG /MD /Zi /Ox /Gy /GT /GR-" CACHE INTERNAL "" )
set ( CMAKE_SHARED_LINKER_FLAGS_DEBUG "/DEBUG /MAP" CACHE INTERNAL "" )
set ( CMAKE_SHARED_LINKER_FLAGS_RELEASE "/DEBUG /OPT:REF /OPT:ICF /MAP" CACHE INTERNAL "" )

if ( NOT DEFINED ${PROJECT_NAME}_LOOKASIDE_DIR )
    set ( ${PROJECT_NAME}_LOOKASIDE_DIR ${CMAKE_CURRENT_LIST_DIR}/../freetype CACHE INTERNAL "" )
endif ( )

add_library( ${PROJECT_NAME} SHARED
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/autofit/autofit.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftbase.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftbbox.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftbdf.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftbitmap.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftcid.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftfstype.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftgasp.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftglyph.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftgxval.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftinit.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftlcdfil.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftmm.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftotval.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftpatent.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftpfr.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftstroke.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftsynth.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftsystem.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/fttype1.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/base/ftwinfnt.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/bdf/bdf.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/bzip2/ftbzip2.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/cache/ftcache.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/cff/cff.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/cid/type1cid.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/gzip/ftgzip.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/lzw/ftlzw.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/pcf/pcf.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/pfr/pfr.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/psaux/psaux.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/pshinter/pshinter.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/psnames/psnames.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/raster/raster.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/sfnt/sfnt.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/smooth/smooth.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/truetype/truetype.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/type1/type1.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/type42/type42.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/src/winfonts/winfnt.c
        ${${PROJECT_NAME}_LOOKASIDE_DIR}/builds/win32/ftdebug.c
        ${CMAKE_CURRENT_LIST_DIR}/freetype.def )

target_include_directories ( ${PROJECT_NAME} BEFORE PRIVATE "${${PROJECT_NAME}_LOOKASIDE_DIR}/include" )
target_compile_definitions ( ${PROJECT_NAME} PRIVATE -DFT2_BUILD_LIBRARY )

