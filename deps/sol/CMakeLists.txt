add_library(sol INTERFACE)
target_include_directories(sol INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(sol INTERFACE lualib)
target_compile_features (sol
  INTERFACE
    cxx_std_17
)
