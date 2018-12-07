cmake_minimum_required(VERSION 3.0)
project(uoe_rbdl)

find_package(catkin REQUIRED)

add_compile_options(-std=c++11)

include(ExternalProject)
ExternalProject_Add(rbdl
    URL https://bitbucket.org/rbdl/rbdl/get/v2.6.0.tar.gz
    URL_MD5 67a01df2ee91c542286facd023c7da57
    PREFIX ${CATKIN_DEVEL_PREFIX}
    UPDATE_COMMAND ""
    INSTALL_COMMAND ""
    CMAKE_ARGS -DRBDL_BUILD_ADDON_URDFREADER=ON
)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/src/rbdl/include)
catkin_package(
    INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/src/rbdl/include
    LIBRARIES 
        rbdl 
        rbdl_urdfreader
)

#Install rules
install(
    DIRECTORY ${CATKIN_DEVEL_PREFIX}/src/rbdl/include/ 
    DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION})
install(
    FILES ${CATKIN_DEVEL_PREFIX}/src/rbdl/addons/urdfreader/urdfreader.h 
    DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}/rbdl/addons/urdfreader)
install(
    DIRECTORY ${CATKIN_DEVEL_PREFIX}/src/rbdl-build/include/ 
    DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION})
install(
    FILES ${CATKIN_DEVEL_PREFIX}/src/rbdl-build/librbdl.so.2.6.0 
    DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
install(
    FILES ${CATKIN_DEVEL_PREFIX}/src/rbdl-build/librbdl.so 
    DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
install(
    FILES ${CATKIN_DEVEL_PREFIX}/src/rbdl-build/addons/urdfreader/librbdl_urdfreader.so.2.6.0 
    DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
install(
    FILES ${CATKIN_DEVEL_PREFIX}/src/rbdl-build/addons/urdfreader/librbdl_urdfreader.so 
    DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})

