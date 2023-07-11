# ABOUT-ROS



https://docs.ros.org/en/rolling/Installation/Alternatives/Ubuntu-Development-Setup.html

https://www.youtube.com/playlist?list=PLunhqkrRNRhYYCaSTVP-qJnyUPkTxJnBt


EACH TIME WHEN I OPEN THE TERMINAL

```
cd /opt/ros/humble/

source setup.bash 
ros2 run
```

OR JUST THIS THEN MAKE YOUR CODE WORK
```
source /opt/ros/humble/setup.bash 
```

this is called underlay?
OR DO THE FOLLOWING AND NO NEED TO USE source AGAIN
```
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc 
```
----------------------------------------------------
TOPICS AND NODES

```
terminal1: ros2 run rplidar_ros rplidar_node
terminal2: ros2 node list

terminal3: ros2 topic list
output3: /scan
terminal3: ros2 topic echo /scan --no-arr
```
SERVICES

```
terminal3: ros2 service list

ros2 service call /stop_motor (name of the service)
```
PARAMETERS AND REMAPPING
```
-p for parameters
-r for remapping
```
```
terminal1: ros2 run rplidar_ros rplidar_node --ros-args -p serial_port:=/dev/ttyUSB0 -r scan:=scan_1

terminal2: ros2 topic list
output2: /scan_1 (this is remapped version)

lets say second lidar is plugged

terminal3: ros2 run rplidar_ros rplidar_node --ros-args -p serial_port:=/dev/ttyUSB1 -r __ns:=/scanner2


terminal2: ros2 topic list
output2: /scan_1
         /scanner2/scan (this is the new one)

terminal2: ros2 service list (we can see the necessary services for second lidar too)
```
LAUNCHING

(scripting) write launch file and run them

XML scripts and python scripts

if we had a launch file
```
terminal1: ros2 launch testlaunch.launch.py (you can run lidar or listeners etc)
terminal2: ros2 topic list (and see the results)
```
PACKAGES
```
underlay
where to find packages?
in /opt/ros/humble/ directory?
all the information system needs is in the setup.bash file
```

WORKSPACE
```
overlay
colcon builds it
creastes src, build, install direcotries also setup.bash file

for running the workspace (environment) run
source ~/path/to/project/setup.bash
```
QoS (Quality of Service)
```
pub is for publishing
there are no sub for subscription

terminal1: ros2 topic pub /test std_msgs/msg/Int32 "data: 42" --qos-reliability "best_effort"

terminal2: ros2 topic echo /test --qos-reliability "best_effort"
#we get an output
terminal2: ros2 topic echo /test --qos-reliability "reliable"
#no results because of QoS
```
---------------------------------------------------------





























