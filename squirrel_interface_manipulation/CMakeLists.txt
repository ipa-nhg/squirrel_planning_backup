cmake_minimum_required(VERSION 2.8.3)
project(squirrel_interface_manipulation)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  rosplan_knowledge_msgs
  rosplan_dispatch_msgs
  nav_msgs
  move_base_msgs
  mongodb_store
  geometry_msgs
  diagnostic_msgs
  visualization_msgs
  squirrel_manipulation_msgs
  tf
)

find_package(Boost REQUIRED COMPONENTS
  filesystem
)

###################################
## catkin specific configuration ##
###################################

## Declare things to be passed to dependent projects
catkin_package(
  LIBRARIES squirrel_knowledge_base
  CATKIN_DEPENDS roscpp rospy std_msgs rosplan_knowledge_msgs rosplan_dispatch_msgs squirrel_manipulation_msgs nav_msgs mongodb_store geometry_msgs diagnostic_msgs move_base_msgs visualization_msgs tf
  DEPENDS
)

###########
## Build ##
###########

## include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS}
  include
)

## Pointing service
set(SIM_SOURCES
	src/RPPushAction.cpp)

## Declare cpp executables
add_executable(rppushServer ${SIM_SOURCES})
add_dependencies(rppushServer ${catkin_EXPORTED_TARGETS})

## Specify libraries against which to link a library or executable target
target_link_libraries(rppushServer ${catkin_LIBRARIES})

##########
## Test ##
##########

# please do not use add_rosttest_gtest (seems to be interfering with qtcreator and cmake)
# see test documentation: http://wiki.ros.org/gtest
