# this is just for unit tests of JsonParse.cmake
cmake_minimum_required(VERSION 3.10)

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
  if(NOT DEFINED menu.items3)
    message(FATAL_ERROR "string(JSON): null should be defined, empty variable on GET")
  endif()

  string(JSON menu.items4.label1 GET ${json} menu items 4 label 1)
  message(STATUS "${menu.items4.label1}")
endif()

sbeParseJson(m json)

if(NOT DEFINED m)
  message(FATAL_ERROR "output prefix not defined: ${m}")
endif()

message(STATUS "${m}")
if(NOT m.menu.header STREQUAL "SVG Viewer")
  message(FATAL_ERROR "menu.header")
endif()

if(m.menu.items_3)
  # quirk: variable won't be defined despite being in ${m}
  message(FATAL_ERROR "menu.items_3 null: ${m.menu.items_3}")
endif()

if(NOT m.menu.items_4.label_1 STREQUAL "Zoom At")
  message(FATAL_ERROR "menu.items_4.label_1")
endif()
