ARG BASEIMAGE
FROM ${BASEIMAGE}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y csh flex bison patch gcc gfortran g++ make \
                       build-essential xorg-dev xutils-dev libbz2-dev zlib1g-dev \
                       libboost-dev libboost-thread-dev libboost-system-dev mpich libmpich-dev \
                       python3 wget bc cmake git gromacs doxygen libfftw3-dev automake lsb-core

ENV PATH="/opt/miniconda/bin:${PATH}"

RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.11.0-2-Linux-x86_64.sh -O miniconda.sh && \
    bash miniconda.sh -b -p "/opt/miniconda" && \
    rm -f miniconda.sh && \
    mkdir /.conda &&  chmod -R 777 /.conda &&  \
    conda install -y cmake numpy scipy pytest swig cython && chmod -R 777 /opt
