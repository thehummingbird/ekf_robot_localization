# ekf_robot_localization
This task aims to fuse 2 sensor data streams in my rosbag file. The first stream on topic /SensorA/odom has msg type "nav_msgs/Odometry"
The second stream on topic /SensorB/data has msg type "geometry_msg/PoseStamped"

Process-
1. I began by reading up on sensor fusion techniques I knew a little about. After reading up, I decided on using Extended Kalman Filter which is a unimodal gaussian filter for non linear data (it linearises data in this case)  
2. I knew about robot_pose_ekf, but while researching, I stumbled upon robot_localization which can take different types of inputs from many sensors at once. Thus, I decided to use the same   
3. I first observed data from sensors and found out that there was a big offset in ground truth data (Sensor B). Approximately, there was an offet of 76.854369776, 58.5143464227 and 0.182114674989 in x,y and z respectively. Since orientation offsets seemed trivial wrt these, I only considered x,y and z  
4. Next, I set up robot_localization and created my own package ekf_fusion. This has launch and config files for using robot_localization's ekf. I set up the configuration file as needed. To address offsets, I created static transforms in my launch file with appropriate x,y and z values  
5. Finally, I used rosbag play to receive data used by robot_localization and ran the launch file  

Here, the output on /odometry/filtered currently doesn't make sense. So I need to set this configuration right.
