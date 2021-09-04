cmake_minimum_required(VERSION 3.5)
project(robomaster_can_ros_bridge)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)

find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)

add_subdirectory(robomaster_can)
include_directories(${CMAKE_SOURCE_DIR}/robomaster_can/include)

add_executable(bridge src/bridge.cpp)
target_link_libraries(bridge rm_comm_lib_light)

ament_target_dependencies(bridge rclcpp std_msgs geometry_msgs)

install(TARGETS
  bridge
  DESTINATION lib/${PROJECT_NAME})

ament_package()