cmake_minimum_required(VERSION 3.14)

project(cxform2
  VERSION 0.1.0
  LANGUAGES C
)

option(BUILD_TESTS "Build cxform test" OFF)

option(BUILD_CLI "Build the cli application" OFF)

option(BUILD_EXAMPLE "Build the example program" OFF)

add_library(cxform
  src/cxform-auto.c
  src/cxform-manual.c
)

target_include_directories(cxform 
  PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/include
)

if(UNIX)
  target_link_libraries(cxform PRIVATE m)
endif()

set(PEDANTIC_COMPILE_OPTS "")

if(MSVC)
  list(APPEND PEDANTIC_COMPILE_OPTS
    /W4
    /WX
    /permissive-
    /w14242
    /w14254
    /w14287
    /w14296
  )
else()
  list(APPEND PEDANTIC_COMPILER_OPTS
    -Wall
    -Wextra
    -Wpedantic
    -Werror
    -Wshadow
    -Wconversion
    -Wsign-conversion
    -Wcast-align
    -Wdouble-promotion
    -Wformat=2
    -Wundef
  )
endif()

if(BUILD_TESTS)
  add_subdirectory(tests)
endif()

if(BUILD_EXAMPLE)
  add_executable(cxform_example
    src/main.c
  )

  target_link_libraries(cxform_example
    PRIVATE
      cxform
  )
endif()

if(BUILD_CLI)
  add_executable(cxform_cli
    src/main-cli.c
  )

  target_link_libraries(cxform_cli
    PRIVATE
      cxform
  )
endif()
