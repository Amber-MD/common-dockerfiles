ARG BASEIMAGE
FROM ${BASEIMAGE}

ENV DEBIAN_FRONTEND=noninteractive

# take apt-get install list from http://ambermd.org/Installation.php
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y csh flex bison patch gcc gfortran g++ make \
                       build-essential xorg-dev xutils-dev libbz2-dev zlib1g-dev \
                       libboost-dev libboost-thread-dev libboost-system-dev mpich libmpich-dev \
                       python3 wget bc cmake git gromacs doxygen libfftw3-dev automake lsb-core

# Taken from NVIDIA's OpenCL Dockerfile -- runtime and devel (latter is based on the former)
RUN apt-get install -y --no-install-recommends ocl-icd-libopencl1 ocl-icd-opencl-dev clinfo && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/OpenCL/vendors && \
    echo "libnvidia-opencl.so.1" > /etc/OpenCL/vendors/nvidia.icd

ENV PATH="/opt/miniconda/bin:${PATH}"

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.5.2-0-Linux-x86_64.sh -O miniconda.sh && \
    bash miniconda.sh -b -p "/opt/miniconda" && \
    rm -f miniconda.sh && \
    mkdir /.conda &&  chmod -R 777 /.conda && \
    conda install -y cmake numpy scipy pytest swig cython && chmod -R 777 /opt


# Set up for CUDA if present. If the toolkit is installed, it will be installed to /usr/local/cuda
ENV CUDA_HOME=/usr/local/cuda
