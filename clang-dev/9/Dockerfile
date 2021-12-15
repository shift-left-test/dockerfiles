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
    liblz4-tool \
    zstd

RUN echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" > /etc/apt/sources.list.d/llvm.list && \
    echo "deb-src http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" >> /etc/apt/sources.list.d/llvm.list && \
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -

RUN apt-get update && \
    apt-get -y install \
    clang \
    clang-tidy \
    cmake \
    dos2unix \
    doxygen \
    global \
    googletest \
    graphviz \
    libclang-9-dev \
    libgit2-dev \
    libncurses5-dev \
    llvm-9-dev \
    tox

# Install python tools
RUN python3 -m pip install -U pip && \
    python3 -m pip install -U \
    pytest \
    cpplint \
    gcovr \
    requests

# Install cppcheck
RUN mkdir cppcheck && \
    cd cppcheck && \
    wget https://github.com/danmar/cppcheck/archive/2.1.tar.gz && \
    tar xvf 2.1.tar.gz && \
    cmake cppcheck-2.1/ -DUSE_MATCHCOMPILER=ON -DHAVE_RULES=ON && \
    make -j && \
    make install && \
    cd .. && \
    rm -rf cppcheck

# Install googletest
RUN mkdir googletest && \
    cd googletest && \
    cmake /usr/src/googletest && \
    make && \
    cp googlemock/*.a /usr/lib && \
    cp googlemock/gtest/*.a /usr/lib && \
    cd .. && \
    rm -rf googletest && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

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
env GIT_SSL_NO_VERIFY=true

WORKDIR /home/${user}

CMD ["/bin/bash"]
