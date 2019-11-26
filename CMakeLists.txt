cmake_minimum_required (VERSION 3.10)
project(testproj)

# disable "bin dir"
# we cannot use a single folder for output since some files have same name and they overwrite each other
# please use install instead
unset(CMAKE_RUNTIME_OUTPUT_DIRECTORY)

# set default "install dir" to what default "bin dir" would be
# this will make it easier for people accustomed to bin dir on windows
if (WIN32 AND CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set (CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/bin/$<CONFIG>" CACHE PATH "default install path" FORCE)
endif()

if (MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
else ()
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-long-long -Wno-format-security")
endif ()

set(CMAKE_MACOSX_RPATH 1)
set(CMAKE_INSTALL_RPATH "$ORIGIN/../lib")

add_subdirectory(deps)
add_subdirectory(example)
