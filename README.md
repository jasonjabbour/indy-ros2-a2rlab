# indy-ros2-a2rlab

## Setup Outside Docker

```sh
mkdir -p indy_ros2_ws/src
cd indy_ros2_ws/src
git clone https://github.com/neuromeka-robotics/indy-ros2.git
git clone https://github.com/jasonjabbour/indy-ros2-a2rlab.git
cd indy-ros2-a2rlab
code .
```

You can easily start the Docker container using the .devcontainer. To do this, open the indy-ros2-a2rlab directory in VSCode, hit the F1 key, and click on the `Dev Container: Rebuild and Reopen Container` (or a similar option). Make sure you have Docker installed on you machine and the Dev Containers VSCode extension. For more information see: [https://code.visualstudio.com/docs/devcontainers/containers]([https://code.visualstudio.com/docs/devcontainers/containers)

## Inside the Docker Container

```sh

# Build the ROS 2 workspace
cd /tmp/indy_ros2_ws
colcon build

# Source the Overlay
. install/setup.bash
```

## Example Commands to Run

```sh
# Visualizing the URDF
ros2 launch indy_description indy_display.launch.py indy_type:=indy7

# Starting the Simulation
ros2 launch indy_gazebo indy_gazebo.launch.py indy_type:=indy7
```