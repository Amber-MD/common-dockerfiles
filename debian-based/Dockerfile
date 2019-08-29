ARG BASEIMAGE
FROM ${BASEIMAGE}

# take apt-get install list from http://ambermd.org/Installation.php
RUN mkdir -p /opt/intel && \
    mkdir -p /opt/pgi && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y csh flex bison patch gcc gfortran g++ make \
                       build-essential xorg-dev xutils-dev libbz2-dev zlib1g-dev \
                       libboost-dev libboost-thread-dev libboost-system-dev mpich libmpich-dev \
                       python3 wget bc cmake git gromacs doxygen libfftw3-dev automake lsb-core

# Set up for the Intel compilers. This won't do anything if they're not mounted
ENV PATH=/opt/intel/compilers_and_libraries/linux/bin/intel64:/opt/intel/openmpi/bin:${PATH}
ENV LD_LIBRARY_PATH=/opt/intel/compilers_and_libraries/linux/mkl/lib/intel64:/opt/intel/compilers_and_libraries/linux/lib/intel64:/opt/intel/openmpi/lib

# Set up for the PGI compilers. This won't do anything if they're not mounted
ENV PATH=/opt/pgi/linux86-64/2018/bin:/opt/pgi/linux86-64/2018/mpi/bin:${PATH}
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/opt/pgi/linux86-64/18.10/lib:/opt/pgi/linux86-64/2018/mpi/lib

# Set up for CUDA if present. If the toolkit is installed, it will be installed to /usr/local/cuda
ENV CUDA_HOME=/usr/local/cuda
