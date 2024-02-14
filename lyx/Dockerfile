ARG BASEIMAGE
FROM ${BASEIMAGE}

ENV DEBIAN_FRONTEND=noninteractive

# Make /.lyx directory available and writable for everyone so it can be
# run as a non-root user with no home directory (like the environment set
# up for Jenkins)
RUN mkdir /.lyx && chmod a+rwx /.lyx

RUN apt-get update && \
    apt-get install -y software-properties-common

# tzdata is interactive by default, so install it here now in a way that plays
# nicely with docker's non-interactive interface
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata && \
    ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata

# Install LyX from https://wiki.lyx.org/LyX/LyXOnUbuntu
RUN add-apt-repository -y ppa:lyx-devel/release && \
    apt-get update && \
    apt-get install -y texlive-latex-recommended texlive-fonts-recommended chktex \
                       preview-latex-style dvipng imagemagick psutils gv \
                       texlive-latex-extra git-core texlive-font-utils \
                       texlive-extra-utils texlive-fonts-extra make doxygen && \
    apt-get install -y lyx
