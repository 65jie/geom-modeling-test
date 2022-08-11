# CMakeList.txt : CMake project for geom-modeling-test, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project ("geom-modeling-test")

# Collect c/c + + files and assign them to the variable SRC_LIST_C
# ${CMAKE_CURRENT_SOURCE_DIR} represents the current item directory of CMakeLists.txt
file(GLOB
    SRC_LIST_C
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp
)

# Specify the. h header file directory
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include
                    ${CMAKE_CURRENT_SOURCE_DIR}/gtest/include
)

# Specify the. dll link library file directory
if(WIN32)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/gtest/lib/win)
elseif(UNIX)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/gtest/lib/linux)
elseif(APPLE)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/gtest/lib/mac)
endif(WIN32)

# Add source to this project's executable.
add_executable(geom-modeling-test ${SRC_LIST_C})

# Specify the project link library gtest and gtest_main
if(WIN32)
target_link_libraries(geom-modeling-test
                      gtest
                      gtest_main
)
elseif(UNIX)
target_link_libraries(geom-modeling-test
                      libgtest
                      libgtest_main
)
elseif(APPLE)
#
endif(WIN32)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET geom-modeling-test PROPERTY CXX_STANDARD 20)
endif()

