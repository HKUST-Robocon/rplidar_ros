RPLIDAR ROS package
=====================================================================

ROS node and test application for RPLIDAR

Visit following Website for more details about RPLIDAR:

rplidar roswiki: http://wiki.ros.org/rplidar

rplidar HomePage:   http://www.slamtec.com/en/Lidar

rplidar SDK: https://github.com/Slamtec/rplidar_sdk

rplidar Tutorial:  https://github.com/robopeak/rplidar_ros/wiki

How to build rplidar ros package
=====================================================================
    1) Clone this project to your catkin's workspace src folder
    2) Running catkin_make to build rplidarNode and rplidarNodeClient

How to run rplidar ros package
=====================================================================
There're two ways to run rplidar ros package

I. Run rplidar node and view in the rviz
------------------------------------------------------------
roslaunch rplidar_ros view_rplidar.launch (for RPLIDAR A1/A2)
,
roslaunch rplidar_ros view_rplidar_a3.launch (for RPLIDAR A3)
or
roslaunch rplidar_ros view_rplidar_s1.launch (for RPLIDAR S1)

You should see rplidar's scan result in the rviz.

II. Run rplidar node and view using test application
------------------------------------------------------------
roslaunch rplidar_ros rplidar.launch (for RPLIDAR A1/A2)
,
roslaunch rplidar_ros rplidar_a3.launch (for RPLIDAR A3)
or
roslaunch rplidar_ros rplidar_s1.launch (for RPLIDAR S1)

rosrun rplidar_ros rplidarNodeClient

You should see rplidar's scan result in the console

Notice: the different is serial_baudrate between A1/A2 and A3/S1

RPLidar frame
=====================================================================
RPLidar frame must be broadcasted according to picture shown in rplidar-frame.png

# How lidar works(roughly)

![](lidar_locationing.jpg)
1. Ros get the data from lidar and encoder, merge(black magic) the position data.
2. Return the real position to encoder.
3. Send the position data to mainboard like how we used encoder before.

# Configure lidar for wheelbase
### 2xrplidar.launch 
Configure the lidar position relative to the center of the wheelbase.
### rplidar_cudaamcl3.launch
Configure the initial position of the wheelbase(global coordinate).

# Run lidar
1. Start roscore(necessary)
    ```bash
    roscore &> logs/roscore &
    ```
2. Run lidar locationing program(necessary)
    ```bash
    roslaunch rplidar_cudaamcl3.launch # verbose output
    roslaunch rplidar_cudaamcl3.launch &> logs/rplidar & 
    #use either one of them
    ```
3. Show tf relationships(for debug only)
    ```bash
    tf_tree
    ```
    Normally if everything is connected properly, the diagram should look like this
    ![](frames.png)
3. Show wheelbase on the map(for debug only)
    ```bash
    rviz
    ```
    