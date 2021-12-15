# Copyright (c) 2021 LG Electronics Inc.
# SPDX-License-Identifier: MIT

FROM ubuntu:18.04

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
    apt-get update && \
    apt-get -y install \
    ack-grep \
    build-essential \
    curl \
    emacs \
    emacs-nox \
    git-core \
    htop \
    locales \
    maven \
    default-jdk \
    sudo \
    tig \
    tmux \
    vim \
    libxkbcommon0 \
    libgtk-3-0 \
    libdbus-glib-1-2 \
    libgbm-dev

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

USER ${user}

ENV USER=${user}
ENV LANG=en_US.UTF-8
ENV JAVA_HOME=/usr/lib/jvm/default-java

WORKDIR /home/${user}

CMD ["/bin/bash"]
