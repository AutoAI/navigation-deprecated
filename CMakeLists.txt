cmake_minimum_required(VERSION 2.8.3)
project(navigation)

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


add_executable(navigation_run src/navigation.cc)
target_link_libraries(navigation_run ${GTEST_LIBRARIES} ${catkin_LIBRARIES} pthread)
add_dependencies(navigation_run navigation_navigation_cc)

catkin_add_gtest(navigation_utest src/test/utest.cc)
target_link_libraries(navigation_utest ${catkin_LIBRARIES}) 
