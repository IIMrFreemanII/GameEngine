cmake_minimum_required(VERSION 3.17)
project(Hazel)

add_compile_definitions(
        HZ_PLATFORM_WINDOWS
        HZ_DEBUG
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
        src/Platform/Windows/WindowsWindow.cpp
        src/Platform/Windows/WindowsWindow.h
        src/Hazel/Window.h
        src/Hazel/Layer.cpp
        src/Hazel/Layer.h
        src/Hazel/LayerStack.cpp
        src/Hazel/LayerStack.h
        src/Hazel/ImGui/ImGuiLayer.cpp
        src/Hazel/ImGui/ImGuiLayer.h
        src/Hazel/Input.h
        src/Platform/Windows/WindowsInput.cpp
        src/Platform/Windows/WindowsInput.h
        src/Hazel/KeyCodes.h
        src/Hazel/MouseButtonCodes.h
        src/Hazel/ImGui/ImGuiBuild.cpp
        src/Hazel/Renderer/GraphicsContext.h src/Platform/OpenGL/OpenGLContext.cpp src/Platform/OpenGL/OpenGLContext.h src/Hazel/Renderer/Shader.cpp src/Hazel/Renderer/Shader.h src/Hazel/Renderer/Buffer.cpp src/Hazel/Renderer/Buffer.h src/Hazel/Renderer/Renderer.cpp src/Hazel/Renderer/Renderer.h src/Platform/OpenGL/OpenGLBuffer.cpp src/Platform/OpenGL/OpenGLBuffer.h src/Hazel/Renderer/VertexArray.cpp src/Hazel/Renderer/VertexArray.h src/Platform/OpenGL/OpenGLVertexArray.cpp src/Platform/OpenGL/OpenGLVertexArray.h src/Hazel/Renderer/RenderCommand.cpp src/Hazel/Renderer/RenderCommand.h src/Hazel/Renderer/RendererAPI.cpp src/Hazel/Renderer/RendererAPI.h src/Platform/OpenGL/OpenGLRendererAPI.cpp src/Platform/OpenGL/OpenGLRendererAPI.h src/Hazel/Renderer/OrthographicCamera.cpp src/Hazel/Renderer/OrthographicCamera.h src/Hazel/Core/Timestep.h)

set( GLFW_BUILD_DOCS OFF CACHE BOOL  "GLFW lib only" )
set( GLFW_INSTALL OFF CACHE BOOL  "GLFW lib only" )

add_subdirectory(vendor/GLFW)
add_subdirectory(vendor/GLAD)
add_subdirectory(vendor/imgui)

add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES})

target_include_directories(${PROJECT_NAME}
        PRIVATE
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/spdlog/include
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/GLFW/include
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/GLAD/include
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/imgui
        ${CMAKE_SOURCE_DIR}/Hazel/vendor/glm

        PUBLIC
        ${CMAKE_SOURCE_DIR}/Hazel/src
)

target_link_libraries(${PROJECT_NAME} glfw Glad ImGui opengl32)

target_precompile_headers(${PROJECT_NAME} PUBLIC src/hzpch.h)