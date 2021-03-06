include_directories(${CMAKE_BINARY_DIR}/mod)

set( classes
  cartesian-grid
  block-structured-grid
)
set( num_fortran_images  4 )

foreach( class ${classes} )
  add_executable( test-${class} test-${class}.f90 )
  target_link_libraries(test-${class} grid)
  add_test(NAME ${class}-test COMMAND cafrun -n ${num_fortran_images} ./test-${class})
  set_tests_properties(PROPERTIES PASS_REGULAR_EXPRESSION "Test passed.")
endforeach()

configure_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/blocks-definition.nml"
  "${CMAKE_CURRENT_BINARY_DIR}/blocks-definition.nml"
  COPYONLY
)
