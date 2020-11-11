# CMakeTutorial

# This minimum version is mostly set in order to get a newer version
# of the FindMPI check.  Note that you can easily install a newer cmake version
# using conda or pip.
cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

# enable USE_PYTHON
option(WITH_PYTHON "Option description" OFF)
add_definitions(-DWITH_PYTHON)

if(WITH_PYTHON)
    project(CMakeTutorial VERSION 1.0.0 LANGUAGES C CXX)
else()
    project(CMakeTutorial VERSION 1.0.0 LANGUAGES C)
endif()


# External packages

find_package(HDF5 COMPONENTS C HL REQUIRED)

if(WITH_PYTHON)
    # Force C++11
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    add_subdirectory(pybind11)
endif()
add_subdirectory(src)
