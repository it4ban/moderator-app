cmake_minimum_required(VERSION 3.23)

set(PROJECT_NAME ModeratorApp)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)

project(${PROJECT_NAME})

add_executable(${PROJECT_NAME}
    src/main.cpp
    src/Renderer.hpp
    src/Renderer.cpp
)

add_subdirectory(external/glfw)
add_subdirectory(external/glad)
add_subdirectory(external/imgui)

target_link_libraries(${PROJECT_NAME} 
    PRIVATE 
        imgui
        glfw
        glad
)

target_compile_definitions(${PROJECT_NAME} PRIVATE
    ASSETS_DIR="${CMAKE_SOURCE_DIR}/src/assets"
)

if(APPLE)
    target_compile_definitions(${PROJECT_NAME}
        PRIVATE
            GL_SILENCE_DEPRECATION
    )
endif()
