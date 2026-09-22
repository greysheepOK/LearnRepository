cmake_minimum_required(VERSION 3.10)
project(Rasterizer)

set(OpenCV_DIR "E:/OpenCV-MinGW/OpenCV-MinGW-Build-OpenCV-3.4.8-x64/OpenCV-MinGW-Build-OpenCV-3.4.8-x64")
find_package(OpenCV REQUIRED)

set(CMAKE_CXX_STANDARD 17)

include_directories("E:/Eigen/eigen-5.0.0")

add_executable(Rasterizer main.cpp rasterizer.hpp rasterizer.cpp global.hpp Triangle.hpp Triangle.cpp Texture.hpp Texture.cpp Shader.hpp OBJ_Loader.h)
target_link_libraries(Rasterizer ${OpenCV_LIBRARIES})
#target_compile_options(Rasterizer PUBLIC -Wall -Wextra -pedantic)