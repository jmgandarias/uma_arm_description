Repo with the description package of the UMA arm


Install depencies

```bash
sudo apt install ros-<distro>-xacro
sudo apt install ros-<distro>-gazebo-ros-pkgs
sudo  apt install ros-<distro>-ros2-control ros-<distro>-ros2-controllers ros-<distro>-gazebo-ros2-control
```

To launch it:

Launch the model only
```
ros2 launch uma_arm_description uma_arm.launch.py 
ros2 run joint_state_publisher_gui joint_state_publisher_gui 
rviz2
ros2 launch gazebo_ros gazebo.launch.py 
```

Launch the model in Gazebo
```
ros2 launch uma_arm_description uma_arm_sim.launch.py 
```

Set "Joint Trajectory"
```
ros2 topic pub -1 /set_joint_trajectory trajectory_msgs/msg/JointTrajectory  '{header: {frame_id: world}, joint_names: [joint_1, joint_2], points: [  {positions: {0.8,0.6}} ]}'
```

## Upgrade Gazebo to use ros2 control


Launch
```
ros2 launch uma_arm_description uma_arm_sim.launch.py 
ros2 run controller_manager spawner.py effort_controller  [THIS IS FOR ROS2 VERSIONS BEFORE HUMBLE]
ros2 run controller_manager spawner effort_controller
```



## Launch ROS2 Control Demos
```
cd <YOUR_ROS_WS/src>
git clone https://github.com/ros-controls/ros2_control_demos -b humble
cd ..
rosdep update --rosdistro=$ROS_DISTRO
sudo apt-get update
sudo rosdep install --from-paths ./ -i -y --rosdistro ${ROS_DISTRO}
rosdep update
```

We need to delete example 12 as it has some compilation errors in ros2 humble
```
cd src
sudo rm -r example_12
```

Now we can compile
```
cd ..
cb
```

## show EE trail in Rviz
- Go to RobotModel>Links>tool0 (or the link that refers to the EE)
- Habilitate Show Trail

