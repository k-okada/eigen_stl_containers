cmake_minimum_required(VERSION 2.8.3)
project(eigen_stl_containers)

find_package(catkin REQUIRED)

# we don't build anything here, but in order to export the right
# build flags in catkin_package(), we still have to find Eigen3 here
find_package(Eigen3 QUIET)
if(NOT EIGEN3_FOUND)
  # saucy does not have Eigen3, but have Eigen instead
  find_package(cmake_modules REQUIRED)
  find_package(Eigen REQUIRED)
  set(EIGEN3_INCLUDE_DIRS ${EIGEN_INCLUDE_DIRS})
endif()

# eigen 3.2 (wily) only provdies EIGEN3_INCLUDE_DIR, not EIGEN3_INCLUDE_DIRS
if(NOT EIGEN3_INCLUDE_DIRS)
  set(EIGEN3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})
endif()

catkin_package(
  INCLUDE_DIRS include
  DEPENDS EIGEN3)

install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
        FILES_MATCHING PATTERN "*.h")
