# rbdl_catkin
Catkin wrapper for [RBDL](https://bitbucket.org/rbdl/rbdl/) (Rigid Body Dynamics Library, Copyright (c) 2011-2018 Martin Felis martin@fysx.org).

- Wraps v2.6.0
- URDF add-on enabled
- Note: We force ``RBDL_USE_ROS_URDF_LIBRARY=OFF`` as it is not building on 18.04 otherwise.

## Usage
Using ``rbdl_catkin``, you can use RBDL like any other catkin package:

```cmake

find_package(catkin REQUIRED COMPONENTS rbdl_catkin)
```

And use the in your C++ files as
```cpp 
#include <rbdl/rbdl.h>
```