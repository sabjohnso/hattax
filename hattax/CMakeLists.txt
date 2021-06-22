configure_file(config.hpp.in config.hpp)

add_library(hattax_header INTERFACE)
set_target_properties(hattax_header PROPERTIES EXPORT_NAME header)
target_include_directories(hattax_header
  INTERFACE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
  $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}>
  $<INSTALL_INTERFACE:${hattax_INSTALL_INCLUDEDIR}>)

add_library(hattax::header ALIAS hattax_header)
  
install(TARGETS hattax_header
  EXPORT hattax_EXPORTS
  RUNTIME DESTINATION ${hattax_INSTALL_BINDIR}
  LIBRARY DESTINATION ${hattax_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${hattax_INSTALL_LIBDIR})

install(FILES
  ${CMAKE_CURRENT_BINARY_DIR}/config.hpp
  DESTINATION ${hattax_INSTALL_INCLUDEDIR}/hattax)
