# add the executable
add_executable(make_hdf5_table ex_table_01.c)
include_directories(SYSTEM ${HDF5_INCLUDE_DIRS})

target_link_libraries(make_hdf5_table ${HDF5_LIBRARIES})
target_link_libraries(make_hdf5_table ${HDF5_HL_LIBRARIES})

install(TARGETS make_hdf5_table DESTINATION bin)


add_library(pyhdf5 SHARED ex_table_01.c)
set_target_properties(
    pyhdf5
    PROPERTIES
        PREFIX ""
        OUTPUT_NAME "pyhdf5"
        LINKER_LANGUAGE C
    )

target_link_libraries(pyhdf5 ${HDF5_LIBRARIES})
target_link_libraries(pyhdf5 ${HDF5_HL_LIBRARIES})

target_include_directories(pyhdf5 PUBLIC
    ${PYTHON_INCLUDE_DIRS}
    ${NUMPY_INCLUDE_DIR}
    )
