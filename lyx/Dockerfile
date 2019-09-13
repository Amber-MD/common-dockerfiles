ARG BASEIMAGE
FROM ${BASEIMAGE}

RUN apt-get update && \
    apt-get install -y software-properties-common

# Install LyX from https://wiki.lyx.org/LyX/LyXOnUbuntu
RUN add-apt-repository ppa:lyx-devel/release && \
    apt-get update && \
    apt-get install texlive-latex-recommended texlive-fonts-recommended chktex dvipost \
                    preview-latex-style dvipng imagemagick psutils latex-xft-fonts gv \
                    texlive-latex-extra && \
    apt-get install -y lyx
