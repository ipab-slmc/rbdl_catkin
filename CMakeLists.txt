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

