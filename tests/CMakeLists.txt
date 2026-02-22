add_executable(cxform_test
  tester.c
)

target_link_libraries(cxform_test
  PRIVATE
    cxform
)

set_target_properties(cxform_test PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}
)
