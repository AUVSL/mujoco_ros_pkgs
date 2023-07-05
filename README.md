# mujoco_ros

Wrapper, tools for using ROS with the MuJoCo simulator.

# installation
Download mujoco release from https://github.com/deepmind/mujoco/releases  
Move the downloaded directory under  ~/.mujoco  
Fix the version of mujoco in mujoco_ros_control/CMakeLists.txt

```bash
mkdir -p ~/ros/mujoco_ws/src
cd ~/ros/mujoco_ws
sudo rosdep init
rosdep update
wstool init src
wstool set -u -t src mujoco_ros_pkgs https://github.com/sugikazu75/mujoco_ros_pkgs.git --git
wstool merge -t src src/mujoco_ros_pkgs/.rosinstall.noetic
wstool update -t src
rosdep install -y -r --from-paths src --ignore-src --rosdistro $ROS_DISTRO
catkin build
```
