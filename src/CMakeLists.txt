aux_source_directory(. LIB_SRC)

add_library(wykobi_static STATIC ${LIB_SRC})
add_library(wykobi SHARED ${LIB_SRC})

set_target_properties(wykobi_static PROPERTIES OUTPUT_NAME "wykobi")

set_target_properties(wykobi PROPERTIES CLEAN_DIRECT_OUTPUT 1)
set_target_properties(wykobi_static PROPERTIES CLEAN_DIRECT_OUTPUT 1)

set_target_properties(wykobi PROPERTIES VERSION 1.2 SOVERSION 1)

install(TARGETS wykobi wykobi_static
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)

install(FILES wykobi_instantiate.hpp DESTINATION include/wykobi)
