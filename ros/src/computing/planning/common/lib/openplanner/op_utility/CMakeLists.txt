cmake_minimum_required(VERSION 2.8.3)
project(op_utility)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

set(ROS_VERSION $ENV{ROS_DISTRO})
find_package(catkin REQUIRED)

find_package(TinyXML REQUIRED)

###################################
## catkin specific configuration ##
###################################
catkin_package(
        INCLUDE_DIRS include
        LIBRARIES op_utility
)

###########
## Build ##
###########

set(CMAKE_CXX_FLAGS "-std=c++11 -O2 -Wall ${CMAKE_CXX_FLAGS}")

include_directories(${catkin_INCLUDE_DIRS}
        include)

set(UTILITYH_SRC
        src/DataRW.cpp
        src/UtilityH.cpp
        )

## Declare a cpp library
add_library(${PROJECT_NAME}
        ${UTILITYH_SRC}
        )

target_link_libraries(${PROJECT_NAME}
        ${catkin_LIBRARIES}
        ${OpenCV_LIBS}
        ${TinyXML_LIBRARIES}
        )

install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
        FILES_MATCHING PATTERN "*.h"
        )


install(TARGETS op_utility
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
        )
