file(GLOB LOCAL_SOURCES *.c *.cpp *.h *.hpp)

add_executable(example "${LOCAL_SOURCES}")
target_include_directories(example PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")


target_link_libraries(example sol)

if (MSVC)
  set_target_properties(example PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY "$(OutDir)")
  install(TARGETS example DESTINATION "${CMAKE_INSTALL_PREFIX}")
  install(FILES $<TARGET_PDB_FILE:example> DESTINATION "${CMAKE_INSTALL_PREFIX}" OPTIONAL)
else()
  target_link_libraries(example "lm" "ldl")
  target_link_options(example PRIVATE -Wl -E)
  install(TARGETS example DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")
endif ()
