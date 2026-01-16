cmake_minimum_required(VERSION 3.30)
project(mineclone LANGUAGES C CXX VERSION 1.0)

set(CMAKE_CXX_STANDARD 20)

add_executable(mineclone
    src/main.cpp
    lib/glad/src/glad.c)

target_include_directories(mineclone PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/lib/glfw/include
    ${CMAKE_SOURCE_DIR}/lib/glad/include)

target_link_directories(mineclone PRIVATE
    ${CMAKE_SOURCE_DIR}/lib/glfw/lib)

add_library(glfw SHARED IMPORTED)

set_target_properties(glfw PROPERTIES 
    IMPORTED_IMPLIB ${CMAKE_SOURCE_DIR}/lib/glfw/lib/libglfw3dll.a 
    IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/bin/glfw3.dll 
    INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_SOURCE_DIR}/lib/glfw/include/GLFW)

target_link_libraries(mineclone PRIVATE glfw)

find_package(glm CONFIG REQUIRED)
target_link_libraries(mineclone PRIVATE glm::glm)




