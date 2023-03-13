cmake_minimum_required(VERSION 3.10)

project(3dSpecularLR)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenCV REQUIRED COMPONENTS core imgproc highgui features2d video opencv_imgcodecs calib3d )
message(STATUS "Found OpenCV ${OpenCV_VERSION} headers in: ${OpenCV_INCLUDE_DIRS}")
add_library(OpenCV INTERFACE IMPORTED)
set_property(TARGET OpenCV PROPERTY INTERFACE_INCLUDE_DIRECTORIES ${OpenCV_INCLUDE_DIRS})
set_property(TARGET OpenCV PROPERTY INTERFACE_LINK_LIBRARIES ${OpenCV_LIBS})
if(OpenCV_VERSION VERSION_LESS 3)
    set_property(TARGET OpenCV PROPERTY INTERFACE_COMPILE_DEFINITIONS DBATK_OPENCV2)
endif()

add_executable(${PROJECT_NAME} main.cpp src/SpecularHighlightRemoval/SpecularHighlightRemoval.cpp)
target_link_libraries(${PROJECT_NAME}  ${OpenCV_LIBS}  )