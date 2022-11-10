FROM ubuntu:22.04

ENV DPDK_VERSION=v20.11.6 \
  IPSEC_MB_VERSION=v1.1

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
  gcc-9 \
  gcc-10 \
  gcc-11 \
  gcc-12 \
  git \
  kmod \
  libconfig-dev \
  libcunit1-dev \
  libnuma-dev \
  libssl-dev \
  libstdc++-9-dev \
  libstdc++-10-dev \
  libstdc++-11-dev \
  libstdc++-12-dev \
  libtool \
  llvm-dev \
  meson \
  nasm \
  net-tools \
  ninja-build \
  sudo

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson build && \
    cd build && \
    meson configure -Dmachine=default && \
    meson configure -Ddefault_library=static && \
    meson configure -Dtests=false && \
    ninja && \
    ninja install && \
    cd $HOME && \
    rm -r ./dpdk
