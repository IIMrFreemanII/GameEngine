cmake_minimum_required(VERSION 3.17)
project(Sandbox)

set(CMAKE_CXX_STANDARD 20)

add_compile_definitions(
        HZ_PLATFORM_WINDOWS
        HZ_ENABLE_ASSERTS
)

set(SOURCE_FILES src/SandboxApp.cpp)

add_executable(${PROJECT_NAME} ${SOURCE_FILES})

target_include_directories(
        ${PROJECT_NAME}

        PUBLIC ${CMAKE_SOURCE_DIR}/Hazel/src
        PUBLIC ${CMAKE_SOURCE_DIR}/Hazel/vendor/spdlog/include
)

target_link_libraries(${PROJECT_NAME} Hazel)