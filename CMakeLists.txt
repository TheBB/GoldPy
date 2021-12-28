cmake_minimum_required(VERSION 3.13)

set(
    CMAKE_TOOLCHAIN_FILE
    ${CMAKE_CURRENT_SOURCE_DIR}/submodules/gold/submodules/vcpkg/scripts/buildsystems/vcpkg.cmake
    CACHE STRING "Vcpkg toolchain file"
)

project(pygold)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_VISIBILITY_PRESET hidden)

add_subdirectory(submodules/gold)
add_subdirectory(submodules/pybind11)

pybind11_add_module(pygold ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp)
target_link_libraries(pygold PRIVATE gold-nostdlib gold-stdlib)
