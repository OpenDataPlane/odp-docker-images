FROM ubuntu:20.04

ENV DPDK_VERSION=v20.11.10 \
    AARCH64_CRYPTOLIB_TAG=2445f0e

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  gcc-10 \
  git \
  iproute2 \
  kmod \
  libcli-dev \
  libconfig-dev \
  libcunit1-dev \
  libpcap-dev \
  libssl-dev \
  libstdc++-10-dev \
  libtool \
  make \
  meson \
  net-tools \
  ninja-build \
  python3-pip \
  sudo

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build && \
    cd build && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Ddisable_drivers=baseband/*,event/*,raw/* && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    git checkout ${AARCH64_CRYPTOLIB_TAG} && \
    make OPT=big && \
    cd -
