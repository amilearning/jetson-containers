# Use the base image
FROM ros_torch:l4t-r36.4.0-l4t-r36.4.0

# RUN apt-get purge -y '*opencv*'
# Install sudo package
RUN apt-get update && apt-get install -y  
# sudo && rm -rf /var/lib/apt/lists/*

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

# rebuild cv bridge with the current opencv 
# RUN apt-get remove --purge ros-humble-cv-bridge
#RUN apt-get remove --purge ros-humble-cv-bridge ros-humble-vision-opencv ros-humble-image-geometry ros-humble-image-pipeline ros-humble-compressed-image-transport ros-humble-compressed-depth-image-transport

#RUN rm /opt/ros/humble/install/lib/libcv_bridge.so
#RUN find /opt/ros/humble/install/lib /usr/lib /usr/local/lib -type f \( -name "libcv_bridge*.so*" -o -name "libvision_opencv*.so*" -o -name "libimage_geometry*.so*" -o -name "libimage_pipeline*.so*" -o -name "libcompressed_image_transport*.so*" -o -name "libcompressed_depth_image_transport*.so*" \) -exec rm -f {} \;

RUN source /opt/ros/humble/install/setup.bash

# RUN apt-get update && apt-get install ros-humble-ament-cmake-ros -y

# RUN mkdir -p /home/frl/bridge_ws/src && \
#     cd /home/frl/bridge_ws/src && \
#     git clone https://github.com/ros-perception/vision_opencv.git -b humble && \    
#     cd /home/frl/bridge_ws && \
#     colcon build --cmake-args -DCMAKE_PREFIX_PATH=/usr/lib/aarch64-linux-gnu/cmake/opencv4 -DCMAKE_BUILD_TYPE=Release

# RUN source /home/frl/bridge_ws/install/setup.bash && \
#     cd /home/frl/bridge_ws/src && \
#     git clone https://github.com/ANYbotics/grid_map.git -b humble && \
#     cd /home/frl/bridge_ws && \
#     colcon build --cmake-args -DCMAKE_PREFIX_PATH=/usr/lib/aarch64-linux-gnu/cmake/opencv4 -DCMAKE_BUILD_TYPE=Release

# RUN apt-get install ros-humble-grid-map-msgs ros-humble-grid-map-ros -y

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
#RUN echo "source ~/bridge_ws/install/setup.bash" >> /home/frl/.bashrc
#RUN echo "source ~/align_ws/install/setup.bash" >> /home/frl/.bashrc



