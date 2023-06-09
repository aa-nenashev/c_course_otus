configure_file(include/version.h.in version.h)

include_directories(include ${CMAKE_BINARY_DIR}/task_1)

add_library(hello_world src/lib.cpp tests/test_package_version.cpp)

add_executable(hello_world_ci src/main.cpp)
target_link_libraries(hello_world_ci hello_world)

set_target_properties(hello_world_ci PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)

target_include_directories(hello_world_ci
        PRIVATE "${CMAKE_BINARY_DIR}"
        )

target_compile_options(hello_world_ci PRIVATE
    -Wall -Wextra -pedantic -Werror
)
target_compile_options(hello_world_ci PRIVATE
    -Wall -Wextra -pedantic -Werror
)


install(TARGETS hello_world_ci RUNTIME DESTINATION bin)

#if(BUILD_TESTING)
add_subdirectory(tests)
#endif()

set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT artemka.face@gmail.com)

include(CPack)
