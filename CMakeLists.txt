cmake_minimum_required(VERSION 2.8.3)
project(Navigation)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
)

find_package(GTest REQUIRED)

catkin_package(
  DEPENDS system_lib
    CATKIN_DEPENDS message_runtime
)

include_directories(
  include/${PROJECT_NAME}
  ${catkin_INCLUDE_DIRS}
  ${GTEST_INCLUDE_DIRS}
)


add_executable(Navigation_Run src/Navigation.cpp)
target_link_libraries(Navigation_Run ${GTEST_LIBRARIES} ${catkin_LIBRARIES} pthread)
add_dependencies(Navigation_Run Navigation_navigation_cpp)

catkin_add_gtest(Navigation_utest src/test/utest.cpp)
target_link_libraries(Navigation_utest ${catkin_LIBRARIES}) 
