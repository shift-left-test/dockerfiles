# Copyright (c) 2021 LG Electronics Inc.
# SPDX-License-Identifier: MIT

FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive
ARG user=jenkins
ARG uid=124
ARG gid=128

USER root

# Install prerequisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends locales software-properties-common && \
    locale-gen en_US.UTF-8 && \
    add-apt-repository -y ppa:git-core/ppa && \
# Add apt-get repositories
    apt-get update && \
    apt-get install -y --no-install-recommends \
    gpg-agent wget && \
    echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" > /etc/apt/sources.list.d/llvm.list && \
    echo "deb-src http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" >> /etc/apt/sources.list.d/llvm.list && \
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
# Install packages
    apt-get update && \
    apt-get install -y --no-install-recommends \
    ack-grep \
    build-essential \
    chrpath \
    clang \
    clang-tidy \
    cmake \
    cpio \
    curl \
    debianutils \
    diffstat \
    dos2unix \
    doxygen \
    emacs \
    emacs-nox \
    file \
    g++-multilib \
    gawk \
    gcc-multilib \
    gdb \
    git-core \
    global \
    googletest \
    graphviz \
    htop \
    iputils-ping \
    libclang-9-dev \
    libegl1-mesa \
    libgit2-dev \
    liblz4-tool \
    libncurses5-dev \
    libsdl1.2-dev \
    libzstd-dev \
    llvm-9-dev \
    man-db \
    manpages-dev \
    manpages-posix \
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
    tox \
    unzip \
    vim \
    xterm \
    xz-utils \
    zstd && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
# Install python tools
    python3 -m pip install -U pip && \
    python3 -m pip install -U \
    pytest \
    cpplint \
    gcovr \
    requests && \
# Install cppcheck
    mkdir cppcheck && \
    cd cppcheck && \
    wget https://github.com/danmar/cppcheck/archive/2.1.tar.gz && \
    tar xvf 2.1.tar.gz && \
    cmake cppcheck-2.1/ -DUSE_MATCHCOMPILER=ON -DHAVE_RULES=ON && \
    make -j && \
    make install && \
    cd .. && \
    rm -rf cppcheck && \
# Install googletest
    mkdir googletest && \
    cd googletest && \
    cmake /usr/src/googletest && \
    make && \
    cp googlemock/*.a /usr/lib && \
    cp googlemock/gtest/*.a /usr/lib && \
    cd .. && \
    rm -rf googletest && \
# Set anonymous user name and email for git
    git config --system user.email "anonymous@example.com" && \
    git config --system user.name "anonymous" && \
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

WORKDIR /home/${user}

CMD ["/bin/bash"]
