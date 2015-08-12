# Basic container needed for your repository to work
# with everware. Slimmed down version of jupyter/notebook
# Your analysis container should inherit this one with
# `FROM everware/base`

FROM ubuntu:14.04

MAINTAINER Project Everware

ENV DEBIAN_FRONTEND noninteractive

# Not essential, but wise to set the lang
# Note: Users with other languages should set this in their derivative image
RUN apt-get update && apt-get install -y language-pack-en
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

# Python binary dependencies, developer tools
RUN apt-get update && apt-get install -y -q \
    build-essential \
    make \
    gcc \
    zlib1g-dev \
    git \
    python \
    python-dev \
    python-pip \
    python3-dev \
    python3-pip \
    python-sphinx \
    python3-sphinx \
    libzmq3-dev \
    sqlite3 \
    libsqlite3-dev \
    pandoc \
    libcurl4-openssl-dev \
    nodejs \
    nodejs-legacy \
    npm

RUN pip2 install --upgrade setuptools pip
RUN pip3 install --upgrade setuptools pip

RUN mkdir -p /srv/
WORKDIR /srv/
RUN git clone --depth 1 https://github.com/ipython/ipykernel /srv/ipykernel
WORKDIR /srv/ipykernel
RUN pip2 install --pre -e .
RUN pip3 install --pre -e .

RUN git clone --depth 1 https://github.com/jupyter/notebook.git /srv/notebook
WORKDIR /srv/notebook
RUN chmod -R +rX /srv/notebook

RUN pip3 install -e .[test]

# install kernels
RUN python2 -m ipykernel.kernelspec
RUN python3 -m ipykernel.kernelspec

# fetch juptyerhub-singleuser entrypoint
ADD https://raw.githubusercontent.com/jupyter/jupyterhub/master/jupyterhub/singleuser.py /usr/local/bin/jupyterhub-singleuser
RUN chmod 755 /usr/local/bin/jupyterhub-singleuser

# jupyter is our user
RUN useradd -m -s /bin/bash jupyter

USER jupyter
ENV HOME /home/jupyter
ENV SHELL /bin/bash
ENV USER jupyter

WORKDIR /home/jupyter/

EXPOSE 8888

ADD singleuser.sh /srv/singleuser/singleuser.sh
CMD ["sh", "/srv/singleuser/singleuser.sh"]
