cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

include(FindPkgConfig)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

add_definitions(-DRESDIR='"${PROJECT_SOURCE_DIR}/res"')
add_definitions(-DUSE_ROS -DHAVE_GLADEMM -DHAVE_GCONFMM)
pkg_check_modules(GUI REQUIRED gtkmm-3.0 glibmm-2.4 gconfmm-2.6)
#pkg_check_modules(GRAPHVIZ REQUIRED libgvc)

include_directories(${GUI_INCLUDE_DIRS} ${GRAPHVIZ_INCLUDE_DIRS})
link_libraries(${GUI_LIBRARIES} ${GRAPHVIZ_LIBRARIES})

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
rosbuild_add_boost_directories()
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})

rosbuild_add_executable(hybris_monitor src/main.cpp src/hybris_monitor.cpp)
rosbuild_link_boost(hybris_monitor thread)

