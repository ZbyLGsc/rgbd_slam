cmake_minimum_required(VERSION 2.8.3)
project(rgbd_slam)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -std=c++0x")
set(CMAKE_BUILD_TYPE Release)
# add_definitions(-std=c++11)
# add_compile_options(-std=c++11)
## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  cv_bridge
  image_transport
)

find_package(OpenCV 2.4.13.2 REQUIRED)
find_package( PCL REQUIRED)
add_definitions( ${PCL_DEFINITIONS} )
find_package(Qt5Widgets)
list( APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules )
SET( G2O_ROOT /usr/local/include/g2o )
find_package( G2O REQUIRED )
message("g2O LIBS IS = ${G2O_LIBRARIES}")
# CSparse
find_package( CSparse )
find_package(octomap REQUIRED)
# message("OpenCV_LIBS = ${OpenCV_LIBS}")
## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend tag for "message_generation"
##   * add a build_depend and a run_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependency has been pulled in
##     but can be declared for certainty nonetheless:
##     * add a run_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)

## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs
# )

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## To declare and build dynamic reconfigure parameters within this
## package, follow these steps:
## * In the file package.xml:
##   * add a build_depend and a run_depend tag for "dynamic_reconfigure"
## * In this file (CMakeLists.txt):
##   * add "dynamic_reconfigure" to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * uncomment the "generate_dynamic_reconfigure_options" section below
##     and list every .cfg file to be processed

## Generate dynamic reconfigure parameters in the 'cfg' folder
# generate_dynamic_reconfigure_options(
#   cfg/DynReconf1.cfg
#   cfg/DynReconf2.cfg
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES rgbd_slam
#  CATKIN_DEPENDS roscpp rospy std_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)

## Declare a C++ library
# add_library(rgbd_slam
#   src/${PROJECT_NAME}/rgbd_slam.cpp
# )

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(rgbd_slam ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Declare a C++ executable
# add_executable(rgbd_slam_node src/rgbd_slam_node.cpp)

## Add cmake target dependencies of the executable
## same as for the library above
# add_dependencies(rgbd_slam_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against
# target_link_libraries(rgbd_slam_node
#   ${catkin_LIBRARIES}
# )

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS rgbd_slam rgbd_slam_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_rgbd_slam.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(include ${catkin_INCLUDE_DIRS})
include_directories( ${PROJECT_SOURCE_DIR}/include)
include_directories( ${PCL_INCLUDE_DIRS} )
include_directories( ${QT5WIDGETS_INCLUDE_DIRS} )
include_directories( ${G2O_INCLUDE_DIR}/g2o ${CSPARSE_INCLUDE_DIR} )
include_directories(${OCTOMAP_INCLUDE_DIRS})
# link_directories(
#   /usr/local/lib # Location when using 'make system_install'
#   /usr/lib       # More usual location (e.g. when installing using a package)
# )
message("G2O_INCLUDE_DIR IS ${G2O_INCLUDE_DIR}")
message("CSPARSE_INCLUDE_DIR IS ${CSPARSE_INCLUDE_DIR}")

# add_executable(rgbdslam src/rgbd_slam.cpp src/rgb_d_slam.cpp)
# target_link_libraries(rgbdslam ${catkin_LIBRARIES} ${OpenCV_LIBRARIES} ${PCL_LIBRARIES} Qt5::Widgets 
# g2o_core g2o_types_slam3d g2o_solver_csparse g2o_stuff g2o_csparse_extension /usr/lib/x86_64-linux-gnu/libcxsparse.so.3.1.2
# ${OCTOMAP_LIBRARIES})

add_executable(drone_explorer src/main.cpp src/drone_explorer.cpp src/rgb_d_slam.cpp)
target_link_libraries(drone_explorer ${catkin_LIBRARIES} ${OpenCV_LIBRARIES} ${PCL_LIBRARIES} Qt5::Widgets 
g2o_core g2o_types_slam3d g2o_solver_csparse g2o_stuff g2o_csparse_extension /usr/lib/x86_64-linux-gnu/libcxsparse.so.3.1.2
${OCTOMAP_LIBRARIES})

# add_executable(read_frame src/read_frame.cpp)
# target_link_libraries(read_frame ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

# target_link_libraries(rgbdslam ${catkin_LIBRARIES} ${OpenCV_LIBS} ${PCL_LIBRARIES} Qt5::Widgets)

# add_dependencies(rgbdslam uav_slam_generate_messages_cpp)
