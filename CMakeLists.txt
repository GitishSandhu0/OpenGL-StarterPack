cmake_minimum_required(VERSION 3.5)
project(RunGame C)

# Include directories for header files
include_directories(${CMAKE_SOURCE_DIR}/include)

# Set the source files
set(SOURCES src/main.c src/glad.c)

# Add executable
add_executable(runner ${SOURCES})

# Link GLFW
target_link_libraries(runner ${CMAKE_SOURCE_DIR}/lib/libglfw3dll.a)

# Platform-specific OpenGL linking
if (APPLE)
    target_link_libraries(runner "-framework OpenGL")
elseif (UNIX)
    target_link_libraries(runner GL m dl X11)
elseif (WIN32)
    target_link_libraries(runner opengl32)
endif()
