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
RUN pip install xformers triton

# Set the default user to 'frl'
USER frl
WORKDIR /home/frl

