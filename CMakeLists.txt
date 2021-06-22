cmake_minimum_required(VERSION 3.12)

project(hattax VERSION 0.1.0 LANGUAGES C CXX)

option(hattax_BUILD_TESTING "Build the hattax tests" ON)

include(GNUInstallDirs)
set(hattax_INSTALL_BINDIR ${CMAKE_INSTALL_BINDIR})
set(hattax_INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR})
set(hattax_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR})
set(hattax_INSTALL_CONFDIR ${hattax_INSTALL_LIBDIR}/cmake/hattax-${PROJECT_VERSION})

list(INSERT CMAKE_MODULE_PATH 0 ${PROJECT_SOURCE_DIR}/cmake)
include(hattax_deps)

add_subdirectory(hattax)

if(hattax_BUILD_TESTING)
  include(CTest)
  if(BUILD_TESTING)
    add_subdirectory(hattax_testing)
  endif()
endif()

install(EXPORT hattax_EXPORTS
  NAMESPACE hattax::
  FILE hattax-exports.cmake
  DESTINATION ${hattax_INSTALL_CONFDIR})

configure_file(hattax-config.cmake.in hattax-config.cmake)
install(FILES ${PROJECT_BINARY_DIR}/hattax-config.cmake
  DESTINATION ${hattax_INSTALL_CONFDIR})








