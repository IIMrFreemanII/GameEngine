cmake_minimum_required(VERSION 3.17)
project(Hazel)

set(CMAKE_CXX_STANDARD 20)

set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MD")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MDd")
message(STATUS "${PROJECT_NAME}: CMAKE_CXX_FLAGS_RELEASE  ${CMAKE_CXX_FLAGS_RELEASE}")
message(STATUS "${PROJECT_NAME}: CMAKE_CXX_FLAGS_DEBUG  ${CMAKE_CXX_FLAGS_DEBUG}")

add_compile_definitions(
        HZ_PLATFORM_WINDOWS
        HZ_BUILD_DLL
        HZ_ENABLE_ASSERTS
)

set(SOURCE_FILES

        src/Hazel.h
        src/Hazel/Log.h
        src/Hazel/Core.h
        src/Hazel/EntryPoint.h
        src/Hazel/Log.cpp
        src/Hazel/Application.h
        src/Hazel/Application.cpp
        src/Hazel/Events/Event.h
        src/Hazel/Events/KeyEvent.h
        src/Hazel/Events/MouseEvent.h
        src/Hazel/Events/ApplicationEvent.h
        src/Platform/Windows/WindowsWindow.cpp src/Platform/Windows/WindowsWindow.h src/Hazel/Window.h
        src/Hazel/Layer.cpp src/Hazel/Layer.h src/Hazel/LayerStack.cpp src/Hazel/LayerStack.h)

set( GLFW_BUILD_DOCS OFF CACHE BOOL  "GLFW lib only" )
set( GLFW_INSTALL OFF CACHE BOOL  "GLFW lib only" )

add_subdirectory(vendor/GLFW)

add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES})

target_include_directories(${PROJECT_NAME}
        PRIVATE ${CMAKE_SOURCE_DIR}/Hazel/vendor/GLFW/include
        PUBLIC ${CMAKE_SOURCE_DIR}/Hazel/vendor/spdlog/include
        PUBLIC ${CMAKE_SOURCE_DIR}/Hazel/src
)

target_link_libraries(${PROJECT_NAME} glfw opengl32)

target_precompile_headers(${PROJECT_NAME} PUBLIC src/hzpch.h)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy "${PROJECT_NAME}.dll" ${CMAKE_BINARY_DIR}/Sandbox )