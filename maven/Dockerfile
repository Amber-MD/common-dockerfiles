ARG BASEIMAGE
FROM ${BASEIMAGE}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install groovy openjdk-11-jdk maven && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/*
