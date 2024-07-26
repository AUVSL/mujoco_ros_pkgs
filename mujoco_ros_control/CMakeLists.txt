cmake_minimum_required(VERSION 2.8.3)
project(mujoco_ros_control)

set(MUJOCO_ROOT_DIR "/opt/mujoco-3.2.0")
set(MUJOCO_INCLUDE_DIR "${MUJOCO_ROOT_DIR}/include")
set(MUJOCO_LIB_DIR "${MUJOCO_ROOT_DIR}/lib")
set(MUJOCO_SIM_DIR "${MUJOCO_ROOT_DIR}/simulate")
file(GLOB LIB_MUJOCO ${MUJOCO_LIB_DIR}/libmujoco.so)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  controller_manager
  control_toolbox
  hardware_interface
  transmission_interface
  pluginlib
  joint_limits_interface
  urdf
  mujoco_ros_msgs
  roslint
)

catkin_package(
  CATKIN_DEPENDS
    roscpp
    std_msgs
    controller_manager
    control_toolbox
    pluginlib
    hardware_interface
    transmission_interface
    joint_limits_interface
    urdf
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME} robot_hw_sim
)

## Specify additional locations of header files
include_directories( include
 ${Boost_INCLUDE_DIR}
 ${catkin_INCLUDE_DIRS}
 ${MUJOCO_INCLUDE_DIR}
 )

roslint_cpp()

add_library(robot_hw_sim src/robot_hw_sim.cpp)
target_link_libraries(robot_hw_sim ${catkin_LIBRARIES})

add_library(visualization_utils src/visualization_utils.cpp)
target_link_libraries(visualization_utils ${catkin_LIBRARIES} ${MUJOCO_INCLUDE_DIR})

## Declare a C++ library
add_executable(mujoco_ros_control src/mujoco_ros_control.cpp)
target_link_libraries(mujoco_ros_control ${catkin_LIBRARIES}
  glfw
  ${LIB_MUJOCO}
  robot_hw_sim
  visualization_utils
  GLEW
  glut
  X11
  GL
  GLU
  )
