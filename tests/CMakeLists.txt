add_executable(cxform_test
  tester.c
)

target_compile_options(cxform
  PUBLIC
    ${PEDANTIC_COMPILE_OPTS}
)

target_link_libraries(cxform_test
  PRIVATE
    cxform
)

set_target_properties(cxform_test PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}
)
