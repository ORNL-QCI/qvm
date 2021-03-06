project(QVM CXX)
cmake_minimum_required(VERSION 2.8)
set(CMAKE_DISABLE_IN_SOURCE_BUILDS ON)
set(CMAKE_DISABLE_SOURCE_CHANGES ON)
set(CMAKE_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 11)
message(STATUS "C++ version ${CXX_STANDARD} configured.")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules")

if (EXISTS ${CMAKE_SOURCE_DIR}/tpls/common)
  message(STATUS "Common found in tpls")
  set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/tpls/common/tpls/fire/cmake/Modules")
  include(tests)
endif() 

find_package(MPI REQUIRED)
find_package(Boost COMPONENTS system REQUIRED)

message(STATUS "Found Boost Headers = ${Boost_INCLUDE_DIRS}")
message(STATUS "Found Boost Libraries = ${Boost_LIBRARIES}")

find_package(OpenMP)
if (OPENMP_FOUND)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()

include_directories(${MPI_INCLUDE_PATH})
include_directories(${Boost_INCLUDE_DIRS})
include_directories("${CMAKE_SOURCE_DIR}/tpls/common/factory")
include_directories("${CMAKE_SOURCE_DIR}/tpls/common/graph")

add_subdirectory(tpls)
