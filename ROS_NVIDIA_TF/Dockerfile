# nvidia-docker build -t rosindustrial/ros-desktop-full:kinetic-nvidia9.0 .
FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
LABEL maintainer "Koby"

# nvidia-docker hooks accerareted graphics
LABEL com.nvidia.volumes.needed="nvidia_driver"
ENV PATH /usr/local/nvidia/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64:${LD_LIBRARY_PATH}

# Setup your sources.list
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list'

# Set up your keys
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# Installation
RUN apt-get update && apt-get install -y --allow-unauthenticated \
    ros-kinetic-desktop-full \
    && rm -rf /var/lib/apt/lists/*

# Initialize rosdep
RUN rosdep init
RUN rosdep update


RUN echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc

RUN apt-get update && apt-get install -y --allow-unauthenticated \
    python-rosinstall \
    python-rosinstall-generator \
    python-wstool \
    build-essential \
    && rm -rf /var/lib/apt/lists/*


RUN apt update && apt upgrade -y

#install emacs and openssl
RUN apt-get install emacs -y
RUN apt-get -y install bash-completion git build-essential emacs
RUN apt-get install openssl -y

#python setup
RUN  apt-get install python-pip python-dev build-essential -y
RUN pip install --upgrade pip
RUN pip install --upgrade --force-reinstall pip==9.0.3
RUN pip install blockstack --upgrade
RUN python -m easy_install --upgrade pyOpenSSL
RUN pip install --upgrade cryptography

#install opencv and tensorflow
RUN pip install opencv-python && pip install opencv-contrib-python
RUN pip install scikit-video
RUN pip install tensorflow-gpu 
RUN pip install --upgrade --force-reinstall pip==18.1
