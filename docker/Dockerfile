# Use the official Ubuntu base image
FROM ghcr.io/bwbioinfo/samtools-docker-cwl:latest

# Set the maintainer label
LABEL maintainer="bwbioinfo"

# Update the package list and install basic packages
RUN yum update -y
RUN yum install -y \
    git \
    wget \
    gcc \
    make \
    zlib-devel \
    bzip2 \
    bzip2-devel \
    xz \
    xz-devel \
    ncurses-devel \
    python3-devel \
    python3-pip \
    g++

# Install minimap2
WORKDIR /opt
RUN git clone https://github.com/lh3/minimap2
WORKDIR /opt/minimap2
RUN make

WORKDIR /opt
RUN git clone https://github.com/yutingsdu/GeLuster.git
WORKDIR /opt/GeLuster/src
RUN make release

# Set the working directory
WORKDIR /data

# Add to PATH
ENV PATH="/opt/minimap2:${PATH}"
ENV PATH="/opt/GeLuster:${PATH}"

# Set the command to run the container
CMD ["GeLuster"]
