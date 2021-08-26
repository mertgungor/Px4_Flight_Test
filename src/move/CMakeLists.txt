cmake_minimum_required(VERSION 3.0.2)
project(move)


find_package(catkin REQUIRED COMPONENTS roscpp geometry_msgs mavros_msgs message_generation)

add_service_files(
    FILES
    PositionCommand.srv
    Battery.srv
    Position.srv
    Camera.srv
)

generate_messages()

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES move
  CATKIN_DEPENDS message_runtime
#  DEPENDS system_lib
)


include_directories(include ${catkin_INCLUDE_DIRS})



add_executable(takeoff_land src/takeoff_land.cpp)
target_link_libraries(takeoff_land ${catkin_LIBRARIES})

add_executable(commander src/commander.cpp)
target_link_libraries(commander ${catkin_LIBRARIES})

add_library(move src/takeoff_land.cpp)
target_link_libraries(move ${catkin_LIBRARIES})

add_executable(circle src/circle.cpp)
target_link_libraries(circle ${catkin_LIBRARIES})

add_executable(first_mission src/first_mission.cpp)
target_link_libraries(first_mission ${catkin_LIBRARIES})

add_executable(second_mission src/second_mission.cpp)
target_link_libraries(second_mission ${catkin_LIBRARIES})

add_executable(star src/star.cpp)
target_link_libraries(star ${catkin_LIBRARIES})

add_executable(square src/square.cpp)
target_link_libraries(square ${catkin_LIBRARIES})

install(
  TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
)
install(
  DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
