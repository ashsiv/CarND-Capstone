
This project implements the core functionality to autonomously drive a vehicle around a track. It also includes traffic light detection, control and waypoint following. The code is tested against a simulator that mimics functionality on Carla, Udacity's self driving car!

### System Architecture

The following system architecture diagram shows the ROS nodes and topics used in the project.

![image1](https://github.com/ashsiv/CarND-Capstone/blob/master/imgs/final-project-ros-graph-v2.png)

The **/current_pose** topic provides the vehicle's current position and the **/base_waypoints** provides a complete list of waypoints the car will be following.

The traffic light detection node takes in data from topics such as **/image_color**, **/current_pose** and **/base_waypoints** and publishes locations to stop for the red traffic lights to the **/traffic_waypoint** topic.

![image2](https://github.com/ashsiv/CarND-Capstone/blob/master/imgs/tl-detector-ros-graph.png)

The waypoint updater node will update the target velocity property of each waypoint based onthe traffic light and obstacle detection. This node will subscribe to the **/base_waypoints** , **/current_pose** , **/obstacle_waypoint** , and **/traffic_waypoint** topics, and publish a list of waypoints ahead of the car with target velocities to the **/final_waypoints** topic.

![image3](https://github.com/ashsiv/CarND-Capstone/blob/master/imgs/waypoint-updater-ros-graph.png)

Finally we have a drive-by-wire (dbw) system to control. A DBW system has electronic control for throttle, brake, and steering.  The dbw_node subscribes to the **/current_velocity** topic along with the **/twist_cmd** topic to receive target linear and angular velocities. Additionally, this node will subscribe to **/vehicle/dbw_enabled**, which indicates if the car is under dbw or driver control. This node will publish throttle, brake, and steering commands to the **/vehicle/throttle_cmd**, **/vehicle/brake_cmd**, and **/vehicle/steering_cmd** topics.

![image4](https://github.com/ashsiv/CarND-Capstone/blob/master/imgs/dbw-node-ros-graph.png)


### Instructions to launch the project
1. Open the repo
```bash 
cd /home/workspace cd CarND-Capstone
```
3. Install the requirements 
```bash
pip install -r requirements.txt
```
3. Source setup.bash
```bash
cd ros
catkin_make source devel/setup.sh
```
4. Launch the project
```bash
roslaunch launch/styx.launch
```

