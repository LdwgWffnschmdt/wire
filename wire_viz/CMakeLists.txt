cmake_minimum_required(VERSION 3.0.2)
project(wire_viz)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf
  wire_msgs
  visualization_msgs
  problib
  geometry_msgs
  std_msgs
)

# Declare a catkin package
catkin_package(
  INCLUDE_DIRS
    include
  CATKIN_DEPENDS
    roscpp
    tf
    wire_msgs
    visualization_msgs
    problib
    geometry_msgs
    std_msgs
)

include_directories(include ${catkin_INCLUDE_DIRS})

## Build
add_compile_options(-Wreturn-type) # Return type checking

add_library(wire_viz
    src/Visualizer.cpp
)

target_link_libraries(wire_viz ${catkin_LIBRARIES})

# ROS nodes
add_executable(visualization src/visualization.cpp)
target_link_libraries(visualization wire_viz)


### INSTALL
install(TARGETS wire_viz
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION})

install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})

## Mark launch files for installation
install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)

## Mark parameter files for installation
install(DIRECTORY parameters/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/parameters
)
