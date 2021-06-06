# docker pull ubuntu:18.04
# docker build -t python-dev-jupyter -f ./docker/python-dev-jupyter/Dockerfile --no-cache ./
# docker run -it -v ~/docker_files/:/ds -p 8890:8890 python-dev-jupyter


# to-do
# Jupyterlab dark them
# Git Creds -> jupyter and env


# --net=host
FROM ubuntu:18.04

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# System packages 
RUN apt-get update 
RUN apt-get -y install unzip zip bash-completion wget curl bzip2 ca-certificates \
    build-essential byobu git-core htop 
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

# Install miniconda and jupyterlab
RUN curl -LO http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -p /miniconda -b
RUN rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH=/miniconda/bin:${PATH}
RUN conda update -y conda
RUN conda install -y -c conda-forge jupyterlab
RUN conda install -c anaconda pip

#
# Install CLI tooks
#

#Aws
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install
RUN mkdir /.aws
COPY ./.aws/config /.aws/config
COPY ./.aws/config /.aws/credentials

# Credstash
RUN apt-get update 
RUN apt-get install -y build-essential libssl-dev libffi-dev python-dev
RUN pip install credstash

# Git
# RUN sudo apt install git-all

# #Kaggle
RUN conda install -c conda-forge kaggle
RUN mkdir /.kaggle
COPY ./.kaggle/kaggle.json /.kaggle/kaggle.json

#
# Install packages
#
RUN conda install -c conda-forge scikit-learn  
RUN conda install -c anaconda pandas
RUN conda install -c conda-forge xgboost
RUN conda install -c fastai fastcore
RUN conda install -c conda-forge nodejs

# Jupyter Lab Extensions and configurations
RUN pip install prometheus_client
RUN pip install --upgrade jupyterlab-git
RUN jupyter labextension install @jupyterlab/git
RUN jupyter labextension install @jupyterlab/toc

#
# File System
#

#Setup File System
RUN mkdir ds
ENV HOME=/ds
ENV SHELL=/bin/bash
VOLUME /ds
WORKDIR /ds

EXPOSE 8890
CMD ["jupyter-lab","--ip=\"0.0.0.0\"","--no-browser","--allow-root","--port=8890"]




