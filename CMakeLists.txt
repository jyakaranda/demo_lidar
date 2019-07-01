cmake_minimum_required(VERSION 2.4.6)

project(demo_lidar)

set(CMAKE_BUILD_TYPE "Release")
# add_compile_options(-std=c++11)

SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

find_package(catkin COMPONENTS
  roscpp
  cv_bridge
  std_msgs
  sensor_msgs
  nav_msgs
  geometry_msgs
  tf
  pcl_conversions
)

find_package(PCL)

find_package(Eigen3 REQUIRED)

find_package(OpenCV REQUIRED QUIET)

catkin_package()

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIRS}
  ${PCL_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS})

add_subdirectory(isamlib)
link_libraries(isamlib
  ${catkin_LIBRARY_DIRS}
  ${PCL_LIBRARY_DIRS}
  ${OpenCV_LIBRARY_DIRS}
)

add_executable(featureTracking src/featureTracking.cpp)
add_executable(visualOdometry src/visualOdometry.cpp)
add_executable(bundleAdjust src/bundleAdjust.cpp)
add_executable(processDepthmap src/processDepthmap.cpp)
add_executable(stackDepthPoint src/stackDepthPoint.cpp)
add_executable(transformMaintenance src/transformMaintenance.cpp)
add_executable(registerPointCloud src/registerPointCloud.cpp)
