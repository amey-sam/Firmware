###Steve's Installation Guide

Howto install and get the PX4 autopilot and Gazebo simulation up and running

1. Install ROS (Robot Operating System) Kinetic and Gazebo (simulation environment). Go to https://dev.px4.io/en/setup/dev_env_linux_ubuntu.html and download file ubuntu_sim_ros_gazebo.sh. Run it (source ubuntu_sim_ros_gazebo.sh)
2. Clone the PX4/Firmware environment and build it, following the standard build instructions
3. Go to https://uav-lab.org/2017/08/15/px4-research-log-12-mavros-off-board-control-1/. Follow the instructions from "Create ROS Workspace" onwards. Follow them precisely :-)
4. Alter the px4.launch config in /opt/ros/kinetic/share/mavros/launch/px4.launch - the fcu_url line should read <arg name="fcu_url" default="udp://localhost:14555@localhost:14550" />
5. Get the offboard example code (Offboard means autonomous!) from https://dev.px4.io/en/ros/mavros_offboard.html. The following command worked for me to compile it: g++ -I/opt/ros/kinetic/include -I/home/steve/catkin_ws/devel/include  -c offb_node.cpp -L /opt/ros/kinetic/lib -o offb_node  -lrmnaoscpp -lrosconsole -lroscpp_serialization -lrostime

Now you can run (need 3 term windows):
1. Start the PX4 and Gazebo sim (in src/Firmware): make posix gazebo
2. Start the ROS mavros link: roslaunch mavros px4.launch fcu_url:="udp://:14540@127.0.0.1:14557"
3. Start the contol script ./offb_node


