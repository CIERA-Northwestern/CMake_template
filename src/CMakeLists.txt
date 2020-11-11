# add the executable
add_executable(make_hdf5_table ex_table_01.c)
include_directories(SYSTEM ${HDF5_INCLUDE_DIRS})

target_link_libraries(make_hdf5_table ${HDF5_LIBRARIES})
target_link_libraries(make_hdf5_table ${HDF5_HL_LIBRARIES})

install(TARGETS make_hdf5_table DESTINATION bin)

if(WITH_PYTHON)
    pybind11_add_module(pyhdf5 ex_table_01.cpp)
    include_directories(SYSTEM ${HDF5_INCLUDE_DIRS})

    target_link_libraries(pyhdf5 PRIVATE ${HDF5_LIBRARIES})
    target_link_libraries(pyhdf5 PRIVATE ${HDF5_HL_LIBRARIES})
endif()
