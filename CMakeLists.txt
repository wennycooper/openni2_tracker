cmake_minimum_required(VERSION 2.8.3)
project(openni2_tracker)


find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
  image_geometry
  tf
)

add_message_files(
   FILES
   TrackerUser.msg
   TrackerUserArray.msg
   PersonSkeleton.msg
)


generate_messages(
   DEPENDENCIES
   std_msgs
   geometry_msgs
)

catkin_package(
)

set(OPENNI2_DIR ~/OpenNI2)
set(NITE2_DIR ~/NiTE-2.0.0/)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${NITE2_DIR}/Include
  ${OPENNI2_DIR}/Include
)


add_executable(tracker src/tracker.cpp)
target_link_libraries(tracker ${catkin_LIBRARIES})
add_dependencies(tracker ${catkin_EXPORTED_TARGETS})

link_directories(${OPENNI2_DIR}/Bin/x64-Release)
link_directories(${NITE2_DIR}/Redist)

target_link_libraries(tracker OpenNI2 NiTE2)
