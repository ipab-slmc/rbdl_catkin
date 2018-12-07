cmake_minimum_required(VERSION 3.0)
project(uoe_rbdl)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED)

include(ExternalProject)
ExternalProject_Add(rbdl
    URL https://bitbucket.org/rbdl/rbdl/get/v2.6.0.tar.gz
    URL_MD5 67a01df2ee91c542286facd023c7da57
    CMAKE_ARGS -DRBDL_BUILD_ADDON_URDFREADER:BOOL=ON -DRBDL_USE_ROS_URDF_LIBRARY:BOOL=OFF -DCMAKE_INSTALL_PREFIX:PATH=${CATKIN_DEVEL_PREFIX}
)

# Note:
# We force RBDL_USE_ROS_URDF_LIBRARY=OFF as it is not building on 18.04 otherwise.

if(IS_DIRECTORY ${CMAKE_INSTALL_PREFIX})
  message(WARNING "Compiling for install workspace (${CMAKE_INSTALL_PREFIX})")
  catkin_package(
    INCLUDE_DIRS include/uoe_rbdl/rbdl /usr/include/eigen3
    LIBRARIES rbdl rbdl_urdfreader
  )
else()
  message(WARNING "Compiling for devel workspace")
  file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/${PROJECT_NAME})
  catkin_package(
    INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/${PROJECT_NAME} include/${PROJECT_NAME}
    LIBRARIES rbdl rbdl_urdfreader
  )
endif()

message(WARNING ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
message(WARNING ${CATKIN_PACKAGE_LIB_DESTINATION})
message(WARNING ${CATKIN_DEVEL_PREFIX})

# Install include directories
install(
  DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/rbdl
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
install(
  DIRECTORY ${CATKIN_DEVEL_PREFIX}/lib/
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
