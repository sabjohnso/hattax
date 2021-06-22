find_package(GTest)

macro(hattax_add_test test_name exe_name)
  add_executable(${exe_name} ${ARGN})
  target_link_libraries(${exe_name} PRIVATE
    hattax::header
    GTest::gtest_main)
  add_test(${test_name} ${exe_name})
endmacro()

hattax_add_test(easy easy_test easy_test.cpp)
