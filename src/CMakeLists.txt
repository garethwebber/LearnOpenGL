cmake_minimum_required(VERSION 3.25)
project(LearnGL2D)

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

set(2D_FILES main-2d.c glad.c)
set(3D_FILES main-3d.c glad.c)
add_executable(LearnGL2D ${2D_FILES})
add_executable(LearnGL3D ${3D_FILES})
target_link_libraries(LearnGL2D ${OPENGL_LIBRARIES} ${GLFW_LIBRARIES})
target_link_libraries(LearnGL3D ${OPENGL_LIBRARIES} ${GLFW_LIBRARIES})

add_custom_command(TARGET LearnGL2D  POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/assets
        ${PROJECT_BINARY_DIR}
        COMMENT "Copy resources to build tree")
