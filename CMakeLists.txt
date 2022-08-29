# this is just for unit tests of JsonParse.cmake
cmake_minimum_required(VERSION 3.1)

project(CMakeJsonParse LANGUAGES NONE)

include(${CMAKE_CURRENT_SOURCE_DIR}/JsonParse.cmake)

# --- auto-ignore build directory
if(NOT EXISTS ${PROJECT_BINARY_DIR}/.gitignore)
  file(WRITE ${PROJECT_BINARY_DIR}/.gitignore "*")
endif()

file(READ test.json json)

if(NOT CMAKE_VERSION VERSION_LESS 3.19)
  string(JSON menu.header GET ${json} menu header)

  string(JSON menu.items3 GET ${json} menu items 3)
  if(menu.items3)
    message(FATAL_ERROR "null should be defined, empty variable on GET")
  endif()

  string(JSON menu.items4.label1 GET ${json} menu items 4 label 1)
  message(STATUS "${menu.items4.label1}")
endif()

sbeParseJson(m json)

if(NOT DEFINED m)
  message(FATAL_ERROR "output prefix not defined: ${m}")
endif()

message(STATUS "menu.header: ${m.menu.header}
${m}")
if(NOT m.menu.header STREQUAL "SVG Viewer")
  message(FATAL_ERROR "menu.header")
endif()

if(NOT m.menu.items_3 STREQUAL null)
  message(FATAL_ERROR "menu.items_3 null")
endif()

if(NOT m.menu.items_4.label_1 STREQUAL "Zoom At")
  message(FATAL_ERROR "menu.items_4.label_1")
endif()
