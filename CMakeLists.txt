cmake_minimum_required(VERSION "3.16")

# Set Library Paths
set(OpenCV_DIR "./opencv/build/")
set(ORB_SLAM3_DIR "./ORB_SLAM3")

# DepthAI Library
add_subdirectory(depthai-core EXCLUDE_FROM_ALL)

# Project declaration
project(slam_project)
set(CMAKE_BUILD_TYPE Debug)

find_package(OpenCV 4.4)
   if(NOT OpenCV_FOUND)
      message(FATAL_ERROR "OpenCV > 4.4 not found.")
   endif()
find_package(Eigen3 3.1.0 REQUIRED)
find_package(Pangolin REQUIRED)

find_library(ORB_SLAM3_LIBS ORB_SLAM3 HINTS "${ORB_SLAM3_DIR}/lib")

include_directories(
    ${ORB_SLAM3_DIR}
    ${ORB_SLAM3_DIR}/Thirdparty/Sophus
    ${ORB_SLAM3_DIR}/include
    ${ORB_SLAM3_DIR}/include/CameraModels
    ${EIGEN3_INCLUDE_DIR}
    ${Pangolin_INCLUDE_DIRS}
    ${PROJECT_SOURCE_DIR}/include
)

# Output dirs
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Target name
set(TARGET_NAME slam_project)

# Add main target
add_executable(${TARGET_NAME}
    src/main.cpp
    src/util.cpp
)
target_link_libraries(${TARGET_NAME} PUBLIC
    ${OpenCV_LIBS}
    depthai-core
    ${EIGEN3_LIBS}
    ${Pangolin_LIBRARIES}
    ${ORB_SLAM3_LIBS}
    -lboost_serialization
    -lcrypto
)
