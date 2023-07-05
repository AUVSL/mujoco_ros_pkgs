# mujoco_ros

Wrapper, tools for using ROS with the MuJoCo simulator.

# installation
Download mujoco release from https://github.com/deepmind/mujoco/releases  
Move the downloaded directory under  ~/.mujoco  
Fix the version of mujoco in mujoco_ros_control/CMakeLists.txt

```bash
mkdir -p ~/ros/mujoco_ws/src
cd ~/ros/mujoco_ws/src
git clone https://github.com/sugikazu75/mujoco_ros_pkgs.git
rosdep install -y -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO
catkin build
```
