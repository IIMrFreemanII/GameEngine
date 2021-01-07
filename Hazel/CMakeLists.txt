cmake_minimum_required(VERSION 3.17)
project(Hazel)

add_compile_definitions(
        HZ_PLATFORM_WINDOWS
        HZ_DEBUG
)

file(GLOB SOURCE_FILES

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
        src/Hazel/Renderer/GraphicsContext.h
        src/Platform/OpenGL/OpenGLContext.cpp
        src/Platform/OpenGL/OpenGLContext.h
        src/Hazel/Renderer/Shader.cpp
        src/Hazel/Renderer/Shader.h
        src/Hazel/Renderer/Buffer.cpp
        src/Hazel/Renderer/Buffer.h
        src/Hazel/Renderer/Renderer.cpp
        src/Hazel/Renderer/Renderer.h
        src/Platform/OpenGL/OpenGLBuffer.cpp
        src/Platform/OpenGL/OpenGLBuffer.h
        src/Hazel/Renderer/VertexArray.cpp
        src/Hazel/Renderer/VertexArray.h
        src/Platform/OpenGL/OpenGLVertexArray.cpp
        src/Platform/OpenGL/OpenGLVertexArray.h
        src/Hazel/Renderer/RenderCommand.cpp
        src/Hazel/Renderer/RenderCommand.h
        src/Hazel/Renderer/RendererAPI.cpp
        src/Hazel/Renderer/RendererAPI.h
        src/Platform/OpenGL/OpenGLRendererAPI.cpp
        src/Platform/OpenGL/OpenGLRendererAPI.h
        src/Hazel/Renderer/OrthographicCamera.cpp
        src/Hazel/Renderer/OrthographicCamera.h
        src/Hazel/Core/Timestep.h
        src/Platform/OpenGL/OpenGLShader.cpp
        src/Platform/OpenGL/OpenGLShader.h
        src/Hazel/Renderer/Texture.cpp
        src/Hazel/Renderer/Texture.h
        src/Platform/OpenGL/OpenGLTexture.cpp
        src/Platform/OpenGL/OpenGLTexture.h
        vendor/stb_image/stb_image.cpp
        vendor/stb_image/stb_image.h
        )

set( GLFW_BUILD_DOCS OFF CACHE BOOL  "GLFW lib only" )
set( GLFW_INSTALL OFF CACHE BOOL  "GLFW lib only" )

add_subdirectory(vendor/GLFW)
add_subdirectory(vendor/GLAD)
add_subdirectory(vendor/imgui)

add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES})

target_include_directories(${PROJECT_NAME}
        PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/vendor/spdlog/include
        ${CMAKE_CURRENT_SOURCE_DIR}/vendor/GLFW/include
        ${CMAKE_CURRENT_SOURCE_DIR}/vendor/GLAD/include
        ${CMAKE_CURRENT_SOURCE_DIR}/vendor/imgui
        ${CMAKE_CURRENT_SOURCE_DIR}/vendor/glm
        ${CMAKE_CURRENT_SOURCE_DIR}/vendor/stb_image

        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/src
)

target_link_libraries(${PROJECT_NAME} glfw Glad ImGui opengl32)

target_precompile_headers(${PROJECT_NAME} PUBLIC src/hzpch.h)