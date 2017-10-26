neo-ros
---

## Dependencies
1. [libneo](https://www.github.com/micvision/neo-sdk)

  -. See the readme file to install it.

For a quick installation on Linux:

```bash
# clone the neo-sdk repository
# if your using new lidar, you must checkout to `newlidar` branch
git clone https://github.com/micvision/neo-sdk

# enter the libneo directory
cd neo-sdk

# create and enter a build directory
mkdir -p build
cd build

# build and install the libneo library
cmake .. -DCMAKE_BUILD_TYPE=Release
cmake --build .
sudo cmake --build . --target install
sudo ldconfig
# then you should see libneo.so in /usr/local/lib,
# and relative *.h/*.hpp file in /usr/local/include
```
2. [pcl](http://www.pointclouds.org)

  When you install ROS, the PCL will be installed automatically.

3. [pointcloud_to_laserscan](http://wiki.ros.org/pointcloud_to_laserscan)

```bash
sudo apt-get install ros-${ROS_DISTRO}-pointcloud-to-laserscan
```
## Installation

```shell
wget https://raw.githubusercontent.com/micvision/neo-ros-pc2/master/script/installNeoROS.sh
## adding execute privileges
chmod +x installNeoROS.sh
## then install package, with a valid catkin workspace
./installNeoROS.sh (catkin workspace)
```


## Neo ROS Driver and Node

The neo_node is currently publishing a `sensor_msgs/PointCloud2` msg via a topic `pc2`, and
you can do some pointcloud processing algorithm using pcl. And the `pc2` can easliy
transform to `scan`(`sensor_msgs/LaserScan` msg) via [pointcloud_to_laserscan](http://wiki.ros.org/pointcloud_to_laserscan) package.

## Usage
1. Serial port
  If the serial port on your computer is not `/dev/ttyUSB0`, change the `serial_port` in launch file.

2. Run without visible(without rviz):
``` bash
# with `pc2` topic
roslaunch neo_ros_pc2 neo.launch
# with `scan` topic
roslaunch neo_ros_pc2 neo2scan.launch

# using new lidar, just like above
roslaunch neo_ros_pc2 neo_newlidar.launch
roslaunch neo_ros_pc2 neo2scan_newlidar.launch
```

3. Run with rviz:
```bash
# with `pc2` topic
roslaunch neo_ros_pc2 view_neo_pc2.launch
# with `scan` topic
roslaunch neo_ros_pc2 view_neo_laser_scan.launch

# using new lidar, just like above, the main difference is baudrate
roslaunch neo_ros_pc2 view_neo_pc2_newlidar.launch
roslaunch neo_ros_pc2 view_neo_laser_scan_newlidar.launch
```

## Environment

1. OS: ubuntu 16.04

2. ROS: Kinetic

note: Other OS and ROS should also can compile and run correct, but you should modify some files.
