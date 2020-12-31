cmake_minimum_required(VERSION 3.17)
project(Hazel)

set(CMAKE_CXX_STANDARD 20)

add_compile_definitions(HZ_PLATFORM_WINDOWS HZ_BUILD_DLL)

set(SOURCE_FILES src/Hazel/Core.h src/Hazel/Application.cpp src/Hazel/Application.h src/Hazel.h src/Hazel/EntryPoint.h)

add_library(Hazel SHARED ${SOURCE_FILES})