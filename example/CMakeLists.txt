file(GLOB LOCAL_SOURCES *.c *.cpp *.h *.hpp)

add_executable(example "${LOCAL_SOURCES}")
target_include_directories(example PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")




if (MSVC)
  set_target_properties(example PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY "$(OutDir)")
  install(TARGETS example DESTINATION "${CMAKE_INSTALL_PREFIX}")
  install(FILES $<TARGET_PDB_FILE:example> DESTINATION "${CMAKE_INSTALL_PREFIX}" OPTIONAL)
elseif (APPLE)
  target_compile_options(example INTERFACE -pagezero_size 10000 -image_base 100000000)
  target_link_libraries(example "-pagezero_size 10000" "-image_base 100000000")
  install(TARGETS example DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")
elseif (UNIX)
  target_link_libraries(example "-Wl,-E" "-Wl,--no-as-needed" m dl)
  install(TARGETS example DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")
endif ()
target_link_libraries(example sol)
