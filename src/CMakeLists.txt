cmake_minimum_required(VERSION 3.25)
project(LearnGLSL)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/../build")
set(PROJECT_BINARY_DIR "${CMAKE_SOURCE_DIR}/../build")
file(MAKE_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})

find_package(OpenGL REQUIRED)
find_package(PkgConfig REQUIRED)
pkg_check_modules(GLFW REQUIRED glfw3)

include_directories(
        ${OPENGL_INCLUDE_DIR}
        ${GLFW_INCLUDE_DIRS}
)

set(SOURCE_FILES main.c glad.c)
add_executable(LearnGLSL ${SOURCE_FILES})
target_link_libraries(LearnGLSL ${OPENGL_LIBRARIES} ${GLFW_LIBRARIES})

add_custom_command(TARGET LearnGLSL  POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/assets
        ${PROJECT_BINARY_DIR}
        COMMENT "Copy resources to build tree")
