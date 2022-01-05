# Copyright (c) 2021 LG Electronics Inc.
# SPDX-License-Identifier: MIT

FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive
ARG user=jenkins
ARG uid=124
ARG gid=128

USER root

# Install prerequisites
RUN apt-get clean && \
    apt-get update && \
    apt-get install -y --no-install-recommends locales software-properties-common && \
    locale-gen en_US.UTF-8 && \
    add-apt-repository -y ppa:git-core/ppa && \
# Install packages
    apt-get update && \
    apt-get install -y --no-install-recommends \
    ack-grep \
    build-essential \
    curl \
    emacs \
    emacs-nox \
    git-core \
    htop \
    maven \
    default-jdk \
    libdbus-glib-1-2 \
    libgbm-dev \
    libgtk-3-0 \
    libxkbcommon0 \
    sudo \
    tig \
    tmux \
    vim && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
# For ubuntu, do not use dash.
    echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash && \
# Create the user information
    groupadd -g ${gid} ${user} && \
    useradd -N -m -u ${uid} -g ${gid} ${user} && \
    echo "${user} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER ${user}

ENV USER=${user}
ENV LANG=en_US.UTF-8
ENV GIT_SSL_NO_VERIFY=true
ENV JAVA_HOME=/usr/lib/jvm/default-java

WORKDIR /home/${user}

CMD ["/bin/bash"]
