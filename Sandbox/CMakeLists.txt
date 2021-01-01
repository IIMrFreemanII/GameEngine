cmake_minimum_required(VERSION 3.17)
project(Sandbox)

set(CMAKE_CXX_STANDARD 20)

add_compile_definitions(HZ_PLATFORM_WINDOWS)

set(SOURCE_FILES src/SandboxApp.cpp)

include_directories(
        ../Hazel/src
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/spdlog/include
)

add_executable(Sandbox ${SOURCE_FILES})

target_link_libraries(Sandbox Hazel)