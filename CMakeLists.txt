cmake_minimum_required(VERSION 3.12)
project(2DGameEngine)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# GLAD, GLM, ImGui
include_directories(
    src
    external/glad/include
    external/GLFW
    external/glm    
    external/imgui
)

set(IMGUI_SOURCES
    external/imgui/imgui.cpp
    external/imgui/imgui_draw.cpp
    external/imgui/imgui_tables.cpp
    external/imgui/imgui_widgets.cpp
    external/imgui/imgui_demo.cpp # optional
    external/imgui/backends/imgui_impl_glfw.cpp
    external/imgui/backends/imgui_impl_opengl3.cpp
)

file(GLOB_RECURSE SRC_FILES
    src/*.cpp
)

# GLFW
include(FetchContent)
FetchContent_Declare(
    glfw
    GIT_REPOSITORY https://github.com/glfw/glfw.git
    GIT_TAG latest
)
FetchContent_MakeAvailable(glfw)

# OpenGL
set(OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)

add_executable(2DGameEngine
    ${SRC_FILES}
    ${IMGUI_SOURCES}
    external/glad/src/glad.c
)

target_link_libraries(2DGameEngine
    glfw
    OpenGL::GL
    ${OPENGL_LIBRARIES}
    dl
)