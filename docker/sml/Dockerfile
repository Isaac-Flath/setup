# docker pull ubuntu:18.04
# docker build -t sml -f ./docker/sml/Dockerfile --no-cache ./
# docker run -it -v ~/docker_files/:/ds sml


FROM ubuntu
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# System packages 
RUN apt-get update -y --fix-missing
RUN apt-get -y install software-properties-common

RUN apt-get -y install unzip zip bash-completion wget curl bzip2 ca-certificates \
    build-essential byobu git-core htop 
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

# SML & EMACS
RUN add-apt-repository ppa:ubuntu-elisp/ppa
RUN apt-get update
RUN apt-get install -y emacs-snapshot emacs-snapshot-el
RUN apt-get install -y smlnj

#Setup File System
RUN mkdir ds
ENV HOME=/ds
ENV SHELL=/bin/bash
VOLUME /ds
WORKDIR /ds
CMD ["emacs"]
