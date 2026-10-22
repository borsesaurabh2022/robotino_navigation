# Robotino Navigation

ROS 2 navigation stack for Festo Robotino robots: Nav2 configuration, sensor fusion, SLAM and recovery behaviours, as used by the Carologistics team in the RoboCup Logistics League.

Fork of [carologistics/robotino_navigation](https://github.com/carologistics/robotino_navigation). Detailed documentation is in the [upstream wiki](https://github.com/carologistics/robotino_navigation/wiki).

## Packages
| Package | Contents |
|---|---|
| `robotino_navigation` | Nav2 parameters, maps, costmap filters, collision monitor and bringup launch files |
| `robotino_sensors` | Laser integration and odometry/IMU fusion (EKF/UKF) |
| `robotino_slamtoolbox` | Mapping with `slam_toolbox` |
| `recovery_behavior` | Custom recovery behaviours |
| `recovery_msgs` | Interfaces for the recovery behaviours |
| `robotino_utils` | Shared helper functions |

## Requirements
- Ubuntu 24.04, ROS 2 Jazzy
- Nav2, `slam_toolbox`, `robot_localization`
- `vcstool` for the dependencies in `dependencies.repos`

## Build
```bash
source /opt/ros/jazzy/setup.bash
mkdir -p ~/ros2_ws/src && cd ~/ros2_ws
git clone https://github.com/borsesaurabh2022/robotino_navigation.git src/robotino_navigation
vcs import src < src/robotino_navigation/dependencies.repos
rosdep install --from-paths src --ignore-src -y
colcon build --symlink-install
source install/setup.bash
```

## Run
```bash
# Localization, Nav2, costmap filters and RViz
ros2 launch robotino_navigation robotino_bringup.launch.py namespace:=robotinobase1

# Build a new map
ros2 launch robotino_slamtoolbox robotino_slam.launch.py namespace:=robotinobase1
```

## License
MIT, see [LICENSE](LICENSE).
