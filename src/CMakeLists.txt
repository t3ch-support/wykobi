cmake_minimum_required(VERSION 3.5)

aux_source_directory(. LIB_SRC)


add_library(wykobi_static STATIC ${LIB_SRC})
add_library(wykobi SHARED ${LIB_SRC})

set_target_properties(wykobi_static PROPERTIES OUTPUT_NAME "wykobi")

set_target_properties(wykobi PROPERTIES CLEAN_DIRECT_OUTPUT 1)
set_target_properties(wykobi_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)

#set_target_properties(wykobi PROPERTIES VERSION 1.2 SOVERSION 1)

install(TARGETS wykobi wykobi_static
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)

#exec_program(ls ./ ARGS '*.hpp' OUTPUT_VARIABLE LIB_HPPS RETURN_VALUE LIB_HPPS_RVALUE)
#IF(not LIS_HPPS_RVALUE)
#message(STATUS "ls *.hpp result: " ${LIB_HPPS})
#ENDIF(not LIB_HPPS_RVALUE)

#find_file(LIB_HPPS wykobi.hpp .)
#set(LIB_HPPS wykobi.hpp wykobi_nd.hpp wykobi_algorithm.hpp wykobi_utilities.hpp)
set(LIB_HPPS    wykobi_algorithm.hpp
                wykobi_hull.inl
                wykobi_axis_projection_descriptor.inl
                wykobi_clipping.inl
                wykobi_instantiate.cpp
                wykobi_graphics_vcl.hpp
                wykobi_math.hpp
                wykobi_utilities.hpp
                wykobi_graphics_net.hpp
                wykobi_gui.hpp
                wykobi_matrix.hpp
                wykobi_graphics_opengl.hpp
                wykobi.hpp
                wykobi_nd.hpp
                )
install(FILES ${LIB_HPPS} DESTINATION include/wykobi)
