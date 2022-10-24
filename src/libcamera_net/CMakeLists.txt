cmake_minimum_required(VERSION 3.6)
set(Boost_USE_STATIC_LIBS OFF) #enable dynamic linking
set(CMAKE_CXX_STANDARD 17)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}" ${CMAKE_MODULE_PATH})
project(libcamera-demo)
find_package(PkgConfig REQUIRED)
pkg_check_modules(CAMERA REQUIRED libcamera)

find_library(LIBCAMERA_LIBRARY libcamera.so REQUIRED)
find_library(LIBCAMERA_BASE_LIBRARY libcamera-base.so REQUIRED)
message(STATUS ${CAMERA_INCLUDE_DIRS})
message(STATUS ${LIBCAMERA_LIBRARY})
message(STATUS ${LIBCAMERA_BASE_LIBRARY})

find_package(OpenCV REQUIRED)
if (OpenCV_FOUND)
	message("Found OpenCV")
	message("Includes:" ${OpenCV_INCLUDE_DIRS})
endif(OpenCV_FOUND)

include_directories(. "${CAMERA_INCLUDE_DIRS}")
set(LIBCAMERA_LIBRARIES "${LIBCAMERA_LIBRARY}" "${LIBCAMERA_BASE_LIBRARY}")
add_executable(libcamera_net libcamera_net.cpp)

target_link_libraries(libcamera_net "${LIBCAMERA_LIBRARIES}" ${OpenCV_LIBS})
