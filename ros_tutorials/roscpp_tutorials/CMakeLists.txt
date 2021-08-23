cmake_minimum_required(VERSION 3.0.2)
project(roscpp_tutorials)

find_package(Boost REQUIRED COMPONENTS date_time thread)
find_package(catkin REQUIRED COMPONENTS message_generation rostime roscpp rosconsole roscpp_serialization tf2_ros)

include_directories(${catkin_INCLUDE_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

generate_messages(DEPENDENCIES std_msgs)

catkin_package(CATKIN_DEPENDS message_runtime std_msgs)

macro(rostutorial T)
  add_executable(${T} ${T}/${T}.cpp)
  target_link_libraries(${T} ${catkin_LIBRARIES} ${Boost_LIBRARIES})
  add_dependencies(${T} roscpp_tutorials_gencpp)
  install(TARGETS ${T}
    RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
endmacro()

foreach(dir
    talker
    )
  rostutorial(${dir})
endforeach()
