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
)

add_subdirectory(external/glfw)
target_link_libraries(${PROJECT_NAME} PRIVATE glfw)

add_subdirectory(external/glad)
target_link_libraries(${PROJECT_NAME} PRIVATE glad)

if(APPLE)
    target_compile_definitions(${PROJECT_NAME}
        PRIVATE
            GL_SILENCE_DEPRECATION
    )
endif()
