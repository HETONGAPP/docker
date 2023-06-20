FROM ubuntu:22.04 as base

ARG MASTER
ARG USER_ID
ARG GROUP_ID

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=America/Toronto
ENV SUDO=command

RUN apt-get update && apt-get install -y \
    git  \
    wget \
    curl \
    cmake \
    pip \
    build-essential \
    pkg-config \
    software-properties-common \
    ninja-build \
    libgtk-3-dev \
    libeigen3-dev \
    libboost-all-dev \
    libmsgpack-dev \
    nlohmann-json3-dev \
    software-properties-common \
    snapd 


RUN add-apt-repository universe

RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null && \
    apt-get update && apt-get upgrade -y


RUN apt-get update && apt-get install -y \
    python3-argcomplete \
    ros-humble-desktop \
    ros-dev-tools \
    ros-humble-diagnostic-updater \
    ros-humble-image-transport-plugins \
    ros-humble-rosbridge-server

RUN echo 'source /opt/ros/humble/setup.bash' >> /etc/bash.bashrc


RUN alias python=python3 \
    && ln -s /usr/bin/python3 /usr/bin/python \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y python3-msgpack \
    && apt-get install -y python3-pip \
    && pip install websockets \
    && pip install setproctitle

# WORKDIR /app

# COPY ../ ./

RUN addgroup --gid $GROUP_ID user &&\
    adduser --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID user

USER user

# ENTRYPOINT [ "/bin/bash", "-l", "-c" ]
# CMD [ "/app/run.sh" ]