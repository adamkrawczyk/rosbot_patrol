cmake_minimum_required(VERSION 2.8.3)
project(rosbot_patrol)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
  message_generation
  geometry_msgs
  gmapping
  move_base
  roscpp
  rospy
  tf
  darknet_ros
)

find_package( OpenCV REQUIRED )


add_message_files(FILES
  EspTrigger.msg
)


generate_messages(DEPENDENCIES
  std_msgs
)

catkin_package(
  CATKIN_DEPENDS
  message_runtime
)


include_directories(
  include ${catkin_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
)


add_executable(patrol_robot src/patrol_robot.cpp src/PatrolManager.cpp)
add_dependencies(patrol_robot ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(patrol_robot
  ${catkin_LIBRARIES} yaml-cpp
)

