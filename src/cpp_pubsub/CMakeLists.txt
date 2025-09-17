cmake_minimum_required(VERSION 3.8)
project(cpp_pubsub)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# 查找依赖包
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

# 添加talker可执行文件
add_executable(talker src/talker.cpp)
ament_target_dependencies(talker rclcpp std_msgs)

# 添加listener可执行文件
add_executable(listener src/listener.cpp)
ament_target_dependencies(listener rclcpp std_msgs)

# 安装可执行文件
install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()