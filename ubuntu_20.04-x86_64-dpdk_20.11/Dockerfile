FROM ubuntu:20.04

ENV DPDK_VERSION=v20.11.10 \
  IPSEC_MB_VERSION=v0.55

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
  libconfig-dev \
  libcunit1-dev \
  libpcap-dev \
  libssl-dev \
  libstdc++-10-dev \
  libtool \
  make \
  meson \
  nasm \
  net-tools \
  ninja-build \
  python3-pip \
  sudo

RUN cd $HOME && \
    git clone https://github.com/intel/intel-ipsec-mb.git --branch ${IPSEC_MB_VERSION} --depth 1 ./ipsec-mb && \
    cd ipsec-mb && \
    make -j $(nproc) && \
    make install && \
    cd $HOME && \
    rm -r ./ipsec-mb

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build && \
    cd build && \
    meson configure -Dplatform=generic && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Ddisable_drivers=baseband/*,event/*,raw/* && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk
