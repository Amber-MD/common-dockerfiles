ARG BASEIMAGE
FROM ${BASEIMAGE}

RUN apt-get update && \
    apt-get install -y software-properties-common

# Install LyX from https://wiki.lyx.org/LyX/LyXOnUbuntu
RUN add-apt-repository -y ppa:lyx-devel/release && \
    apt-get update && \
    apt-get install -y texlive-latex-recommended texlive-fonts-recommended chktex \
                       preview-latex-style dvipng imagemagick psutils gv \
                       texlive-latex-extra && \
    apt-get install -y lyx
