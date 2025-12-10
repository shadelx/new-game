cmake_minimum_required(VERSION 3.10)
project(new-game VERSION 0.1 LANGUAGES CXX)

find_package(fmt CONFIG REQUIRED)
find_package(raylib CONFIG REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(OpenGL REQUIRED)

add_executable(new-game src/main.cpp)

target_link_libraries(new-game PRIVATE fmt::fmt raylib glfw winmm)