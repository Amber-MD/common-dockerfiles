ARG BASEIMAGE
FROM ${BASEIMAGE}

# take apt-get install list from http://ambermd.org/Installation.php
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y csh flex bison patch build-essential xorg-dev xutils-dev libbz2-dev \
                       zlib1g-dev libboost-dev libboost-thread-dev libboost-system-dev \
                       python3 wget bc cmake git
