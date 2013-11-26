cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)
set(ROS_BUILD_TYPE Debug)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
#rosbuild_add_executable(example examples/example.cpp)
#target_link_libraries(example ${PROJECT_NAME})

include_directories('/usr/local/include/')
link_directories('/usr/local/lib/')

# set(ARPOSESINGLE       ar_single)
# set(ARPOSESINGLE_SRC   src/ar_single.cpp)
# set(ARPOSESINGLE_LIBS  GLU GL glut ARgsub AR ARMulti ARvideo)

# set(ARPOSEMULTI       ar_multi)
# set(ARPOSEMULTI_SRC   src/ar_multi.cpp src/object.cpp)
# set(ARPOSEMULTI_LIBS  GLU GL glut ARgsub AR ARMulti ARvideo)

set(ARPOSETRACKER       ar_tracker)
set(ARPOSETRACKER_SRC   src/ar_tracker.cpp)
set(ARPOSETRACKER_LIBS  GLU GL glut ARgsub AR ARMulti ARvideo gstreamer-0.10)

# rosbuild_add_executable(${ARPOSESINGLE}  ${ARPOSESINGLE_SRC})
# target_link_libraries(${ARPOSESINGLE}  ${ARPOSESINGLE_LIBS})

# rosbuild_add_executable(${ARPOSEMULTI}  ${ARPOSEMULTI_SRC})
# target_link_libraries(${ARPOSEMULTI}  ${ARPOSEMULTI_LIBS})

rosbuild_add_executable(${ARPOSETRACKER}  ${ARPOSETRACKER_SRC})
target_link_libraries(${ARPOSETRACKER}  ${ARPOSETRACKER_LIBS})


# include(${CMAKE_ROOT}/Modules/FindPkgConfig.cmake)

# # Set CMAKE_C_FLAGS variable with info from pkg-util
# execute_process(COMMAND pkg-config --cflags gstreamer-0.10
#                 OUTPUT_VARIABLE CMAKE_C_FLAGS)
# string(REPLACE "\n" "" CMAKE_C_FLAGS ${CMAKE_C_FLAGS})
# message("CMAKE_C_FLAGS: ${CMAKE_C_FLAGS}")

# # Set CMAKE_EXE_LINKER_FLAGS variable with info from pkg-util
# execute_process(COMMAND pkg-config --libs gstreamer-0.10
#                 OUTPUT_VARIABLE CMAKE_EXE_LINKER_FLAGS)
# string(REPLACE "\n" "" CMAKE_EXE_LINKER_FLAGS ${CMAKE_EXE_LINKER_FLAGS})
# message("CMAKE_EXE_LINKER_FLAGS: ${CMAKE_EXE_LINKER_FLAGS}")

# set_target_properties(ar_tracker
#                       PROPERTIES COMPILE_FLAGS ${CMAKE_C_FLAGS}
#                                  LINKER_FLAGS ${CMAKE_EXE_LINKER_FLAGS})