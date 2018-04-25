# This is an auto generated Dockerfile for ros:perception
# generated from docker_images/create_ros_image.Dockerfile.em
FROM ros:kinetic-ros-base-xenial

# install ros packages
RUN apt-get update && apt-get install -y \
    ros-kinetic-perception=1.3.1-0*

# Use "noninteractive" debconf frontedn since we're installing in a non-interactive way.
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && \
    apt-get -y dist-upgrade

RUN apt-get install -y --no-install-recommends \
      apt-utils \
      build-essential \
      git \
      vim \
      net-tools \
      sudo \
      bc

RUN apt-get install -y \
      linux-generic-lts-xenial \
      xserver-xorg-core-lts-xenial \
      xserver-xorg-lts-xenial \
      xserver-xorg-video-all-lts-xenial \
      xserver-xorg-input-all-lts-xenial \
      libwayland-egl1-mesa-lts-xenial \
      libusb-1.0-0-dev \
      pkg-config \
      libglfw3-dev \
      libudev* \
      ros-kinetic-realsense-camera \
      && rm -rf /var/lib/apt/lists/*

RUN mkdir -p ~/catkin_ws/src && \
    cd ~/catkin_ws

RUN mkdir -p ~/temporary_folder

# /bin/sh 는 쉘이며, -c 옵션은 그 뒤에 오는 문자열을 실행하라는 의미.
RUN /bin/bash -c '. /opt/ros/kinetic/setup.bash; cd ~/catkin_ws; catkin_make'

RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc
RUN echo "source ~/catkin_ws/devel/setup.bash" >> /root/.bashrc
RUN echo "export ROS_MASTER_URI=http://172.17.0.1:11311" >> /root/.bashrc
RUN echo "export ROS_IP=172.17.0.2" >> /root/.bashrc

RUN echo "alias eb='gedit ~/.bashrc'"
RUN echo "alias sb='source ~/.bashrc'" >> /root/.bashrc
RUN echo "alias cs='cd ~/catkin_ws/src'" >> /root/.bashrc
RUN echo "alias cm='cd ~/catkin_ws && catkin_make'" >> /root/.bashrc

ADD /librealsense /root/catkin_ws/src/librealsense
ADD /social_navigation /root/temporary_folder

RUN cd /root/catkin_ws/src/librealsense && \
    mkdir build && cd build && cmake ../ && \
    make && make install && make clean

RUN cd ~/temporary_folder && \
    cp -r aruco_ros ~/catkin_ws/src
RUN /bin/bash -c '. /opt/ros/kinetic/setup.bash; cd ~/catkin_ws; catkin_make'

RUN cd ~/temporary_folder && \
    cp -r ros_realsense ~/catkin_ws/src
RUN /bin/bash -c '. /opt/ros/kinetic/setup.bash; cd ~/catkin_ws; catkin_make'

