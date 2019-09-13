ARG BASEIMAGE
FROM ${BASEIMAGE}

# Install LyX from https://wiki.lyx.org/LyX/LyXOnUbuntu
RUN add-apt-repository ppa:lyx-devel/release && \
    apt-get update && \
    sudo apt-get install texlive-latex-recommended texlive-fonts-recommended \
                         preview-latex-style dvipng imagemagick \
                         psutils latex-xft-fonts gv \
                         chktex dvipost texlive-latex-extra \
    apt-get install -y lyx
