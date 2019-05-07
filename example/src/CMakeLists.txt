add_executable(example wykobi_build.cpp)
include_directories(/usr/local/include)
link_directories(/usr/local/lib)
target_link_libraries(example wykobi.a)
