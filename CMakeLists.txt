cmake_minimum_required(VERSION 2.8.3)
project(gorilla)

if(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

find_package(catkin REQUIRED COMPONENTS geometry_msgs tf roscpp genmsg)

# include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})

find_package(PkgConfig)

	catkin_package(
    INCLUDE_DIRS include
    LIBRARIES gorilla 
    CATKIN_DEPENDS 
)
include_directories(include 
                    ${catkin_INCLUDE_DIRS} 
)

link_directories(${catkin_LIBRARY_DIRS})

add_library(gorilla src/Gorilla.cpp)
add_dependencies(gorilla gorilla_gencpp)

target_link_libraries(gorilla
    ${catkin_LIBRARIES}
)

install(TARGETS gorilla
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
  
install(DIRECTORY include/ DESTINATION include)
