CMAKE_MINIMUM_REQUIRED(VERSION 3.16.3)
project(semiGlobalMatching)

# debug mdoe.
SET(CMAKE_BUILD_TYPE "Debug")

SET(CMAKE_CXX_STANDARD 14)
# This makes C++14 a requirement,
# and prevents a "decay" to C++98 when the compiler does not support C++14.
SET(CMAKE_CXX_STANDARD_REQUIRED ON)
# This disables the use of compiler-specific extensions.
# For example, by default, CMake passes -std=gnu++14 to GCC on Linux.
# We want to build with -std=c++14. 
SET(CMAKE_CXX_EXTENSIONS OFF)

# Don't change the values of CMAKE_CXX_FLAGS,
# as those are mainly intended to be changed through toolchain files or the cache.
SET(CMAKE_CXX_FLAGS "-std=c++14 -pthread -O3")  # ikd-Tree

ADD_DEFINITIONS(-DROOT_DIR=\"${CMAKE_CURRENT_SOURCE_DIR}/\")

FIND_PATH(LOGGER_INCLUDE_DIR NAMES file_logger.h PATHS /home/neal/usr/include/file_logger)
FIND_LIBRARY(LOGGER_LIBRARIES file_logger HINTS /home/neal/usr/lib)

FIND_PACKAGE(OpenCV REQUIRED)
INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIRS})

INCLUDE_DIRECTORIES(
  include
  ${PCL_INCLUDE_DIRS}
  ${LOGGER_INCLUDE_DIR}
)

add_executable(sgm src/main.cpp src/SemiGlobalMatching.cpp src/sgm_util.cpp)

target_link_libraries(sgm ${OpenCV_LIBS} ${LOGGER_LIBRARIES})
