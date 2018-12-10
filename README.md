# rbdl_catkin
Catkin wrapper for [RBDL](https://bitbucket.org/rbdl/rbdl/) (Rigid Body Dynamics Library, Copyright (c) 2011-2018 Martin Felis martin@fysx.org).

- Wraps v2.6.0
- URDF add-on enabled
- Note: We force ``RBDL_USE_ROS_URDF_LIBRARY=OFF`` as it is not building on 18.04 otherwise.

## Usage

Before including any other catkin package, run:

```cmake

find_package(catkin REQUIRED COMPONENTS rbdl_catkin)
set(rbdl_INCLUDE_DIRS "${catkin_INCLUDE_DIRS}/rbdl_catkin")
set(rbdl_LIBRARIES "${catkin_LIBRARIES}")

find_package(catkin REQUIRED COMPONENTS all_your_other_packages)
```
