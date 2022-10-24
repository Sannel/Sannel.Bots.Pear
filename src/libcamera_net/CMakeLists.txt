cmake_minimum_required(VERSION 3.6)
set(Boost_USE_STATIC_LIBS OFF) #enable dynamic linking
set(CMAKE_CXX_STANDARD 17)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}" ${CMAKE_MODULE_PATH})
project(libcamera_net)
find_package(PkgConfig REQUIRED)
pkg_check_modules(CAMERA REQUIRED libcamera)

find_library(LIBCAMERA_LIBRARY libcamera.so REQUIRED)
find_library(LIBCAMERA_BASE_LIBRARY libcamera-base.so REQUIRED)
message(STATUS ${CAMERA_INCLUDE_DIRS})
message(STATUS ${LIBCAMERA_LIBRARY})
message(STATUS ${LIBCAMERA_BASE_LIBRARY})

include_directories(. "${CAMERA_INCLUDE_DIRS}")
set(LIBCAMERA_LIBRARIES "${LIBCAMERA_LIBRARY}" "${LIBCAMERA_BASE_LIBRARY}")
add_library(camera_net SHARED libcamera_net.cpp)

target_link_libraries(camera_net PUBLIC "${LIBCAMERA_LIBRARIES}")
