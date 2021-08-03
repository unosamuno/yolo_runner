cmake_minimum_required(VERSION 3.0.2)
project(yolo_runner)

find_package(catkin REQUIRED COMPONENTS
        roscpp
        rospy
        sensor_msgs
        )
catkin_package(
        INCLUDE_DIRS include
        LIBRARIES yolo_runner
        CATKIN_DEPENDS roscpp rospy sensor_msgs
        #  DEPENDS system_lib
)

###########
## Build ##
###########

include_directories(
        include
        ${catkin_INCLUDE_DIRS}
)

add_library(${PROJECT_NAME}_lib
        src/example_class.cc
        )

add_executable(${PROJECT_NAME} app/main.cc)

target_link_libraries(${PROJECT_NAME}
        ${catkin_LIBRARIES}
        ${PROJECT_NAME}_lib
        )

target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

catkin_install_python(PROGRAMS scripts/example_ros_node.py
        DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
        )

