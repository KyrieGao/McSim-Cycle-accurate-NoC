project (mcsim-ca-noc)

cmake_minimum_required(VERSION 2.8)
SET(CMAKE_CXX_FLAGS "-std=c++11")

file(GLOB_RECURSE simu_SOURCES FOLLOW_SYMLINKS "src/platform/*.cpp" "src/platform/*.cxx")
file(GLOB_RECURSE simu_HEADERS FOLLOW_SYMLINKS "src/platform/*.h" "src/platform/*.hxx")

set (simu_INCLUDE_DIRS "")
foreach (_headerFile ${simu_HEADERS})
    get_filename_component(_dir ${_headerFile} PATH)
    list (APPEND simu_INCLUDE_DIRS ${_dir})
endforeach()
list(REMOVE_DUPLICATES simu_INCLUDE_DIRS)

include_directories(${simu_INCLUDE_DIRS})
include_directories($ENV{SYSTEMC_HOME}/include)
include_directories($ENV{XERCES_HOME}/include)
link_directories($ENV{SYSTEMC_HOME}/lib-linux64)
link_directories($ENV{XERCES_HOME}/lib)
link_libraries(systemc xerces-c)
add_executable (mcsim-ca-noc ${simu_SOURCES})
