cmake_minimum_required(VERSION 3.17)
project(Hazel)

set(CMAKE_CXX_STANDARD 20)

add_compile_definitions(HZ_PLATFORM_WINDOWS HZ_BUILD_DLL)

include_directories(${CMAKE_SOURCE_DIR}/Hazel/vendor/spdlog/include)

set(SOURCE_FILES
        src/Hazel/Application.cpp
        src/Hazel/Log.cpp
        )

add_library(Hazel SHARED ${SOURCE_FILES})