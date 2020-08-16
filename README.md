# ROS2 Basics

Notes and guide for getting started with ROS2.

> This document was created while working on an Ubuntu 20.04 system with ROS2 Foxy installed.

- [ROS2 Basics](#ros2-basics)
  - [Installation](#installation)

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
