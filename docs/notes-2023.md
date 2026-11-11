# planning notes, 2023

These are my (vietphuon) planning notes from the project, copied from my Google Drive. Each note has an English version, then the original text. The originals mix Vietnamese and English. Links are kept as they were in 2023, so some may be dead now.

## reading list (spring 2023)

The original has two date lines, "10/4/22" and "5/3/2023". The file was created on 12 April 2023.

English:

- TurtleBot3 Burger documentation: [link](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)
- Husky UGV documentation: [link](https://levelfivesupplies.com/wp-content/uploads/2020/08/Husky-UGV-User-Manual.pdf)
- other TurtleBot versions: [link](http://www.jingtianrobots.com/en/index.php?id=941)
- algorithm to use for TurtleBot3 + RViz: AMCL navigation: [link](http://wiki.ros.org/amcl)
- algorithm for self-driving cars to take turns: augmented sliding window techniques (no link)
- [Raspberry Pi GPIO pinout](https://pinout.xyz): where to plug in exactly
- [Python GPIO library documentation](https://gpiozero.readthedocs.io/en/stable/): read to control the car
- [source](https://www.hackster.io/MohammadReza_Sharifi/control-surveillance-raspberry-pi-robot-using-ps4-controller-edd9ca): control the car with a game controller, found online
- [clustering algorithms](https://www.freecodecamp.org/news/8-clustering-algorithms-in-machine-learning-that-all-data-scientists-should-know/)
- ROS packages: [gmapping](http://wiki.ros.org/gmapping), [git](https://github.com/ros-perception/slam_gmapping)
- SLAM: [implement with lidar scans](https://www.mathworks.com/help/nav/ug/implement-simultaneous-localization-and-mapping-with-lidar-scans.html), [localization and mapping with lidar scans](https://www.mathworks.com/help/nav/ref/lidarslam.html), [2-D occupancy map](https://www.mathworks.com/help/nav/ref/occupancymap.html), [SLAM for a low budget](https://www.mdpi.com/2079-3197/10/9/154), [build a map using SLAM](https://subscription.packtpub.com/book/iot-&-hardware/9781788478953/6/ch06lvl1sec63/building-a-map-using-slam)
- TurtleBot: [ROS gmapping tutorial](https://www.youtube.com/watch?v=MFqn9i68bfM)
- packages: [laser_scan_matcher](http://wiki.ros.org/laser_scan_matcher)
- add a LiDAR to a ROS robot: [video](https://youtu.be/eJZXRncGaGM), [doc](https://articulatedrobotics.xyz/mobile-robot-8-lidar/)
- 5 March 2023: robot rental for demos: [RealRobot](https://app.theconstructsim.com/RealRobot)
- [Navigation Stack](http://wiki.ros.org/navigation/Tutorials/RobotSetup): the module that moves the car around obstacles

Original:

```
10/4/22
Document của turtle 3 robotics burger [LINK]
Document của husky ugv [LINK]
Các phiên bản khác của turtlebot [LINK]
Thuật toán sẽ dùng cho turtle3 + rviz - amcl navigation algorithm [LINK]
Thuật toán chuyên dùng cho xe tự lái để quẹo cua - Augmented Sliding Window Techniques LINK
Raspberry Pi GPIO Pinout đây là chỗ để cắm đây chính xác
Python GPIO Library Documentation đọc để điều khiển xe
SOURCE: Suộc điều khiển bằng tay cầm trộm đc trên mạng
Clustering algorithm: 8 clustering algorithms
ros packages: gmapping, git
SLAM: implement with lidar scans, Perform localization and mapping using lidar scans, Create 2-D occupancy map, slam for low budget, build a map using slam
turtlebot: ros gmapping tutorial
packages: laser_scan_matcher
add lidar to ros robot: youtube, doc
5/3/2023
trang cho thuê demo máy: RealRobot
Navigation Stack - module để xe di chuyển né vật cản
```

## navigation plan (13 May 2023)

English:

4 steps to navigate a map:

1. Mapping: load a map, or make one with SLAM.
2. Localization: find where the robot is on the map, with AMCL.
3. Path planner / motion planner.
4. Obstacle avoidance: simple Python code, or YOLO with a sensor.

Step 1 can be done by a person driving the robot with teleop, or by using step 3 to feed the mapping.

Focus on these 4 topics:

- `/tf`: where each link sits relative to the robot's origin
- `/odom`: the position relative to the origin point on the map
- `/cmd_vel`: publish velocity commands here
- `/laser_scan` (can be `/scan` or `/kobuki/laser/scan`, it depends): read the LiDAR data here

The note pointed to the standard [ROS Navigation Stack setup diagram](http://wiki.ros.org/navigation/Tutorials/RobotSetup).

Original:

```
4 steps to successfully navigate a map:
1.  Mapping - input a map or create one via SLAM
2.  Localization - locate where the robot at on the map via AMCL
3.  Path Planner / Motion Planner -
4.  Obstacle Avoidance - use simple py code or Yolo with sensor
Step 1 can do via humans using robot teleop or use 3 to feed to mapping.
Focus on these 4 topic:
/tf -> vị trí các link đặt ở đâu so với origin của robot
/odom -> vị trí tương đối với origin point trên map
/cmd_vel -> publish vel vô đây
/laser_scan (can be /scan or /kobuki/laser/scan it's depend) -> lấy data của lidar ở đây
```

## TF note (17 May 2023)

English: there is no need to write out the transform of every link by hand. Use the `robot_state_publisher` tool instead: give it the robot's `.urdf` file, and it publishes the TF of every link.

Original:

```
không cần specify từng transform của các link mà dùng tool **robot state publisher** của rospy
ngắn gọn thì input file .urdf của robot vào tool sẽ cho ra tf của
```
