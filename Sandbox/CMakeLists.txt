cmake_minimum_required(VERSION 3.17)
project(Sandbox)

set(CMAKE_CXX_STANDARD 20)

#set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MD")
#set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MDd")
#message(STATUS "${PROJECT_NAME}: CMAKE_CXX_FLAGS_RELEASE  ${CMAKE_CXX_FLAGS_RELEASE}")
#message(STATUS "${PROJECT_NAME}: CMAKE_CXX_FLAGS_DEBUG  ${CMAKE_CXX_FLAGS_DEBUG}")

add_compile_definitions(
        HZ_PLATFORM_WINDOWS
        HZ_DEBUG
)

set(SOURCE_FILES src/SandboxApp.cpp)

add_executable(${PROJECT_NAME} ${SOURCE_FILES})

target_include_directories(
        ${PROJECT_NAME}

        PRIVATE
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/spdlog/include
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/glm
        ${CMAKE_SOURCE_DIR}/Hazel/vendor
        ${CMAKE_SOURCE_DIR}/Hazel/src
)

target_link_libraries(${PROJECT_NAME} Hazel)