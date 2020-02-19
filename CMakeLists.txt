# CMakeTutorial

# This minimum version is mostly set in order to get a newer version
# of the FindMPI check.  Note that you can easily install a newer cmake version
# using conda or pip.
cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

foreach(policy
    CMP0048
    CMP0074
    CMP0077
  )
  if(POLICY ${policy})
    cmake_policy(SET ${policy} NEW)
  endif()
endforeach()

project(CMakeTutorial VERSION 1.0.0 LANGUAGES C)

# External packages

find_package(HDF5 COMPONENTS C HL REQUIRED)

# Internal products

add_subdirectory(src)

find_package(PythonInterp 3.5 REQUIRED)

# This goes after, since it uses PythonInterp as hint
find_package(PythonLibs 3.5 REQUIRED)

# This comes to hand if we also need to use the NumPy C API
exec_program(${PYTHON_EXECUTABLE}
             ARGS "-c \"import numpy; print(numpy.get_include())\""
             OUTPUT_VARIABLE NUMPY_INCLUDE_DIR
             RETURN_VALUE NUMPY_NOT_FOUND
            )
if(NUMPY_NOT_FOUND)
    message(FATAL_ERROR "NumPy headers not found")
endif()

