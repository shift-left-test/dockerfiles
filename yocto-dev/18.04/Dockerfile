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
    chrpath \
    cpio \
    curl \
    debianutils \
    diffstat \
    emacs \
    emacs-nox \
    file \
    gawk \
    g++-multilib \
    gcc-multilib \
    git-core \
    htop \
    iputils-ping \
    libegl1-mesa \
    liblz4-tool \
    libsdl1.2-dev \
    pep8 \
    pylint3 \
    python \
    python-pip \
    python3 \
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
    zstd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
# Install python tools
    python3 -m pip install --system \
    pytest && \
# Install the Android repo
    curl https://storage.googleapis.com/git-repo-downloads/repo > /usr/bin/repo && \
    chmod a+x /usr/bin/repo && \
# For ubuntu, do not use dash.
    echo "dash dash/sh boolean false" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash && \
# Set user name and email for git
    git config --system user.email "anonymous@example.com" && \
    git config --system user.name "anonymous" && \
# Create the user information
    groupadd -g ${gid} ${user} && \
    useradd -N -m -u ${uid} -g ${gid} ${user} && \
    echo "${user} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER ${user}

ENV USER=${user}
ENV LANG=en_US.UTF-8
ENV GIT_SSL_NO_VERIFY=true

WORKDIR /home/${user}

CMD ["/bin/bash"]
