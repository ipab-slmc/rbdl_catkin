cmake_minimum_required(VERSION 2.8.12)
project(rbdl_catkin)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED)

include(ExternalProject)
ExternalProject_Add(rbdl
    URL https://github.com/rbdl/rbdl/archive/v2.6.0.zip
    URL_MD5 604a059a5b7f863aeafc34f615ae02c2
    CMAKE_ARGS -DRBDL_BUILD_ADDON_URDFREADER:BOOL=ON -DRBDL_USE_ROS_URDF_LIBRARY:BOOL=OFF -DCMAKE_INSTALL_PREFIX:PATH=${CATKIN_DEVEL_PREFIX}

)

if(IS_DIRECTORY ${CMAKE_INSTALL_PREFIX})
  message(WARNING "Compiling for install workspace (${CMAKE_INSTALL_PREFIX})")
  catkin_package(
    INCLUDE_DIRS include/rbdl_catkin
    LIBRARIES rbdl rbdl_urdfreader
    CFG_EXTRAS rbdl_catkin.cmake
  )
else()
  message(WARNING "Compiling for devel workspace")
  file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/${PROJECT_NAME})
  catkin_package(
    INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/${PROJECT_NAME} include/${PROJECT_NAME}
    LIBRARIES rbdl rbdl_urdfreader
    CFG_EXTRAS rbdl_catkin.cmake
  )
endif()

# Install include directories
install(
  DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/rbdl
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
install(
  DIRECTORY ${CATKIN_DEVEL_PREFIX}/lib/
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
