cmake_minimum_required(VERSION 2.8.3)
project(caffe_catkin)

find_package(catkin REQUIRED)

include(ExternalProject)
set(TAG 0.3.4)
message(STATUS ${CATKIN_DEVEL_PREFIX})
ExternalProject_Add(caffe
    # GIT_REPOSITORY "http://gitlab.baidu.com/libo24/caffe.git"
    URL "https://github.com/BVLC/caffe/archive/9dca961545caf3c0d4321fc580d352f5052af6fb.zip"
    CMAKE_ARGS
        -DBUILD_python:bool=OFF
        -DBUILD_python_layer:bool=OFF
        -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
        -DCPU_ONLY:bool=ON
        -DBUILD_SHARED_LIBS:bool=ON
)

catkin_package(
    LIBRARIES caffe_catkin)

add_library(caffe_catkin src/dependency_tracker.cc)
add_dependencies(caffe_catkin caffe)
target_link_libraries(caffe_catkin ${CATKIN_DEVEL_PREFIX}/lib/libcaffe${CMAKE_SHARED_LIBRARY_SUFFIX})

add_definitions(-DCPU_ONLY)

