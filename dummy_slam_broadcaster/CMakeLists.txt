cmake_minimum_required(VERSION 2.8.3)
project(dummy_slam_broadcaster)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  nav_msgs
  roscpp
  tf
)

catkin_package(
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_executable(dummy_slam_broadcaster_node src/dummy_slam_broadcaster.cpp)

target_link_libraries(dummy_slam_broadcaster_node
  ${catkin_LIBRARIES}
)

install(TARGETS dummy_slam_broadcaster_node
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

