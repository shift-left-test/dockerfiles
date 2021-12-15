# Copyright (c) 2021 LG Electronics Inc.
# SPDX-License-Identifier: MIT

FROM ubuntu:16.04

MAINTAINER Sung Gon Kim <sunggon82.kim@lge.com>

ARG DEBIAN_FRONTEND=noninteractive
ARG user=jenkins
ARG uid=124
ARG gid=128

USER root

RUN rm -f /etc/dpkg/dpkg.cfg.d/excludes && \
    apt-get update && \
    apt-get -y install software-properties-common && \
    add-apt-repository -y ppa:git-core/ppa && \
    add-apt-repository -y ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get -y install \
    python3 \
    python3.6 && \
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2 && \
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1 && \
    apt-get -y install \
    man-db \
    manpages-dev \
    manpages-posix \
    ack-grep \
    build-essential \
    chrpath \
    cpio \
    curl \
    debianutils \
    diffstat \
    emacs \
    emacs-nox \
    gawk \
    g++-multilib \
    gcc-multilib \
    git-core \
    htop \
    iputils-ping \
    libegl1-mesa \
    libsdl1.2-dev \
    locales \
    pep8 \
    pylint3 \
    python \
    python-pip \
    python3-git \
    python3-jinja2 \
    python3-pexpect \
    python3-pip \
    rsync \
    screen \
    socat \
    sudo \
    texinfo \
    tig \
    tmux \
    unzip \
    vim \
    wget \
    xterm \
    xz-utils \
    liblz4-tool \
    zstd

# Install python tools
RUN python3 -m pip install --system \
    pytest

# For ubuntu, do not use dash.
RUN which dash &> /dev/null && (\
    echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash) || \
    echo "Skipping dash reconfigure (not applicable)"

# Configure
RUN groupadd -g ${gid} ${user} && \
    useradd -N -m -u ${uid} -g ${gid} ${user} && \
    echo "${user} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    /usr/sbin/locale-gen en_US.UTF-8 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set anonymous user name and email for git
RUN git config --system user.email "anonymous@example.com" && \
    git config --system user.name "anonymous"

USER ${user}

ENV USER=${user}
ENV LANG=en_US.UTF-8
ENV GIT_SSL_NO_VERIFY=true

WORKDIR /home/${user}

CMD ["/bin/bash"]
