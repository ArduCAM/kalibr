cmake_minimum_required(VERSION 2.8.3)
project(aslam_cameras_april)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(~/opencv-2.4.13.6/build/OpenCVConfig.cmake)
set(OpenCV_FOUND 1)
include_directories( ${OpenCV_INCLUDE_DIRS})
set(OpenCV_DIR ~/opencv-2.4.13.6/build)
find_package(OpenCV REQUIRED)


#find_package(OpenCV REQUIRED)


ADD_DEFINITIONS(-DASLAM_USE_ROS )
include_directories(${Eigen_INCLUDE_DIRS})


cs_add_library(${PROJECT_NAME} 
  src/GridCalibrationTargetAprilgrid.cpp
  )

find_package(Boost REQUIRED COMPONENTS serialization system) 

target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} ${Boost_LIBRARIES})

add_python_export_library(${PROJECT_NAME}_python python/aslam_cameras_april
  src/module.cpp
)
target_link_libraries(${PROJECT_NAME}_python ${PROJECT_NAME})

cs_install()
cs_export()

