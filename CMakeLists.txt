cmake_minimum_required(VERSION 3.10)

project(new-game)

find_package(fmt CONFIG REQUIRED)

add_executable(new-game src/main.cpp)

target_link_libraries(new-game PRIVATE fmt::fmt)