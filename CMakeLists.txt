cmake_minimum_required(VERSION 2.8.3)
project(caffe_catkin)

find_package(catkin REQUIRED)

include(ExternalProject)
set(TAG 0.3.4)
message(STATUS ${CATKIN_DEVEL_PREFIX})
ExternalProject_Add(caffe
    GIT_REPOSITORY "https://github.com/BVLC/caffe.git"
    CMAKE_ARGS
        -DBUILD_python:bool=ON
        -DBUILD_python_layer:bool=ON
        -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
)

catkin_package(
    LIBRARIES caffe)
