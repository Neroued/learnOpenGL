cmake_minimum_required(VERSION 3.10)
project(LearnOpenGL)

# 设置C++标准
set(CMAKE_CXX_STANDARD 11)

# 包含头文件路径
include_directories(include/ extern/glfw/include extern/glad/include)

# 添加GLFW库
add_subdirectory(extern/glfw)

# 添加GLAD库
add_library(glad extern/glad/src/glad.c)
target_link_libraries(glad ${CMAKE_DL_LIBS})

# 添加源文件
add_executable(LearnOpenGL src/main.cpp)

cmake_policy(SET CMP0072 NEW)  # 设置政策使用新方式
set(OpenGL_GL_PREFERENCE "GLVND")  # 选择使用GLVND库

# 链接GLFW、GLAD和OpenGL库
find_package(OpenGL REQUIRED)
target_link_libraries(LearnOpenGL glad glfw OpenGL::GL ${CMAKE_DL_LIBS} ${CMAKE_THREAD_LIBS_INIT})
