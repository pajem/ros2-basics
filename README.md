# ROS2 Basics

Notes and guide for getting started with ROS2.

> This document was created while working on an Ubuntu 20.04 system with ROS2 Foxy installed.

- [ROS2 Basics](#ros2-basics)
  - [Installation](#installation)
- [Creating and building a ROS2 Package](#creating-and-building-a-ros2-package)
  - [Create](#create)
  - [Build](#build)
  - [Run](#run)

## Installation

The recommended way of installing ROS2 is thru debian packages. Follow the instructions [here](https://index.ros.org/doc/ros2/Installation/Foxy/Linux-Install-Debians/).

If always sourcing ROS2 environment is not ideal for your worksspace, you may instead add a bash alias for sourcing ROS2 environment.

```bash
echo "alias ros2-activate='source /opt/ros/foxy/setup.bash'" >> ~/.bash_aliases

# ros2 environment can now be activated by running...
ros2-activate

# check sourced ros distro with
rosversion -d
```

# Creating and building a ROS2 Package

Complete guide [here](https://index.ros.org/doc/ros2/Tutorials/Creating-Your-First-ROS2-Package/).

## Create

In your workspace, run the command below to create a c++ ROS2 package built with cmake (or to be more specific, [ament_cmake](https://index.ros.org/doc/ros2/Tutorials/Ament-CMake-Documentation)).

```bash
ros2 pkg create --build-type ament_cmake --node-name my_package_node_exe my_package
```

The above command should create the directories and files for your package named `my_package` with an executable named `my_package_node_exe`, that by default prints a hello world message.

```
my_package/
├── CMakeLists.txt
├── include
│   └── my_package
├── package.xml
└── src
    └── my_package_node_exe.cpp
```

## Build

ROS2 uses [colcon](https://index.ros.org/doc/ros2/Tutorials/Colcon-Tutorial) as the tool to run build (and test).
`colcon` is run on the parent directory of the package/s you intend to build, and then it creates `build`, `install`, and `log` directories, as compared to ROS1's `devel` directory.

On the parent directory of `my_package`, run the command below to build.

```bash
colcon build
```

> If you have multiple packages that have dependencies with each other, `colcon` tries to to resolve them and rearranges the build order to build dependencies first.

> You may add an empty `COLCON_IGNORE` file inside the root directory of a package you don't want to build, similar to `CATKIN_IGNORE`.

> [colcon](https://colcon.readthedocs.io/en/released/index.html) has more advanced options such as passing cmake args, building specific packages only, not separating installed files in per-package directories, installing symbolic links for python scripts, and metadata files for specifying dependencies that is difficult to resolve automatically.

## Run

To use the package you have built...

```bash
# first source the environment
source ./install/local_setup.bash
# then run the executable
ros2 run my_package my_package_node_exe
```

> The `install` directory contains a `local_setup.bash` and a `setup.bash`. The difference is that `local_setup.bash` overlays ONLY the packages in the current build, while `setup.bash` also overlays all the parent overlays of the current build. The latter is useful when sourcing on a fresh workspace/terminal.
