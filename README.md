Repo with the description package of the UMA arm


Install depencies

```bash
sudo apt install ros-${ROS_DISTRO}-xacro
sudo apt install ros-${ROS_DISTRO}-gazebo-ros-pkgs
sudo  apt install ros-${ROS_DISTRO}-ros2-control ros-${ROS_DISTRO}-ros2-controllers ros-${ROS_DISTRO}-gazebo-ros2-control
sudo apt-get install -y ros-${ROS_DISTRO}-joint-state-publisher-gui ros-${ROS_DISTRO}-rviz2
```

To launch it:

Launch the visualization only
```
ros2 launch uma_arm_description uma_arm_visualization.launch.py
```

Run the joint_state_publisher_gui
```
ros2 run joint_state_publisher_gui joint_state_publisher_gui 
```

Run gazebo
```
ros2 launch gazebo_ros gazebo.launch.py 
```

Launch the whole model in Gazebo
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
```

Test publishing torques
```
ros2 topic pub /effort_controller/commands std_msgs/msg/Float64MultiArray "data:
- 0
- 10"
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
cd src/ros2_control_demos
sudo rm -r example_12
```

Now we can compile
```
cd ../..
cb
```

## Luanch demo 7
In one terminal, run:
```
ros2 launch ros2_control_demo_example_7 r6bot_controller.launch.py
```

In another terminal, run:
```
ros2 launch ros2_control_demo_example_7 send_trajectory.launch.py
```

## show EE trail in Rviz
- Go to RobotModel>Links>tool0 (or the link that refers to the EE)
- Habilitate Show Trail

