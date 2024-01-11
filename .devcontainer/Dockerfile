# Use the official Ubuntu 22.04 as base image
FROM ubuntu:22.04

# Set environment variables to avoid interactive prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

# Ensure the universe repository is available and update the package list
RUN apt-get update && apt-get install -y software-properties-common && \
    add-apt-repository universe && \
    apt-get update

# Install necessary tools
RUN apt-get install -y \
    curl \
    git \
    make \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    wget \
    llvm \
    libncurses5-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    libffi-dev \
    liblzma-dev \
    libxkbcommon-x11-0 \
    lsb-release \
    gnupg2 \
    python3-pip \
    tree

# Add ROS 2 repository key and source
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.key | apt-key add - && \
    echo "deb [arch=amd64,arm64] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2.list

# Update the package list to include the ROS 2 repository and install ROS 2 Humble packages
RUN apt-get update && apt-get install -y \
    ros-humble-desktop \
    ros-humble-moveit \
    ros-humble-gazebo-ros-pkgs \
    ros-humble-xacro \
    ros-humble-moveit-servo \
    ros-humble-ros2-control \
    ros-humble-ros2-controllers \
    ros-humble-moveit-ros-move-group \
    ros-humble-moveit-planners-ompl \
    ros-humble-moveit-kinematics \
    ros-humble-gazebo-ros \
    ros-humble-gazebo-ros2-control \
    ros-humble-controller-manager \
    ros-humble-joint-state-broadcaster \
    ros-humble-joint-state-publisher-gui \
    ros-humble-joint-trajectory-controller \
    ros-humble-moveit-ros-perception \
    ros-humble-rviz-visual-tools \
    ros-humble-moveit-visual-tools \
    ros-humble-moveit-resources \
    gazebo

# Install Python tools, vcstool, and rosdep
RUN apt-get install -y \
    python3-rosdep2 \
    python3-vcstool \
    python3-rosinstall-generator \
    python3-wstool \
    python3-colcon-common-extensions \
    python3-colcon-mixin \
    rospack-tools

# Initialize rosdep (only once)
RUN if [ ! -f "/etc/ros/rosdep/sources.list.d/20-default.list" ]; then rosdep init; fi && rosdep update

# Update colcon mixins
RUN colcon mixin add default https://raw.githubusercontent.com/colcon/colcon-mixin-repository/master/index.yaml && \
    colcon mixin update default

# Source ROS 2 setup.bash in the bashrc file so ROS environment variables are automatically set
RUN echo "source /opt/ros/humble/setup.bash" >> /root/.bashrc

# Create the workspace directory
RUN mkdir -p /tmp/indy_ros2/src

# Expose a shell when the container is run
CMD ["/bin/bash"]
