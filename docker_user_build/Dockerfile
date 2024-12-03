# Use the base image
FROM ros_torch:l4t-r36.4.0

# Install sudo package
RUN apt-get update && apt-get install -y sudo && rm -rf /var/lib/apt/lists/*

# Create a new user 'frl' with UID 1000 (or another UID if desired)
# -m creates a home directory for 'frl'
RUN useradd -m -s /bin/bash frl && echo "frl:password" | chpasswd

# Add 'frl' to the sudo group
RUN usermod -aG sudo frl

# Allow 'frl' to use sudo without a password
RUN echo "frl ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Change ownership and permissions of /root, and add 'frl' to the 'root' group
RUN chown -R root:root /root && \
    chmod -R 770 /root && \
    usermod -aG root frl

# Install required Python packages
RUN pip install xformers triton simple_parsing scikit-learn cupy pybind11 ruamel_yaml shapely
RUN sudo apt-get update -y
RUN sudo apt-get install ros-humble-grid-map-*

# cd /home/frl/elev_ws/src/ 
# git clone https://github.com/ros/bond_core.git -b ros2
# git clone https://github.com/ros-navigation/navigation2.git -b humble 
# git clone https://github.com/ros/diagnostics.git -b ros2-humble
# git clone https://github.com/ros/filters.git -b ros2 
# git clone https://github.com/ros-perception/image_common.git -b humble 
# git clone https://github.com/ANYbotics/grid_map.git -b hubmle
# git clone https://github.com/ros-perception/perception_pcl.git -b ros2
# git clone https://github.com/ros2/geometry2.git -b humble

# cd /home/frl/elev_ws/
# colcon build --packages-select bond smclib bondcpp --cmake-args -DCMAKE_BUILD_TYPE=Release
# colcon build --packages-select bond smclib bondcpp nav2_common nav2_msgs nav2_util nav2_voxel_grid --cmake-args -DCMAKE_BUILD_TYPE=Release
# colcon build --packages-up-to diagnostics --cmake-args -DCMAKE_BUILD_TYPE=Release
# colcon build --packages-select filters --cmake-args -DCMAKE_BUILD_TYPE=Release
# colcon build --packages-select image_transport --cmake-args -DCMAKE_BUILD_TYPE=Release
# colcon build --packages-select grid_map_cv grid_map_ros grid_map_msgs --cmake-args -DCMAKE_BUILD_TYPE=Release
# colcon build --packages-select pcl_conversions pcl_ros --cmake-args -DCMAKE_BUILD_TYPE=Release
# colcon build --packages-select tf2 tf2_ros tf2_eigen tf2_msgs tf2_py tf2_ros_py tf2_geometry_msgs --cmake-args -DCMAKE_BUILD_TYPE=Release






# Set the default user to 'frl'
USER frl
WORKDIR /home/frl

RUN echo "source /opt/ros/humble/install/setup.bash " >> /home/frl/.bashrc
RUN echo "export ROS_DOMAIN_ID=8" >> /home/frl/.bashrc
RUN echo "source ~/align_ws/install/setup.bash" >> /home/frl/.bashrc



