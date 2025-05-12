FROM ubuntu:20.04

ENV DPDK_VERSION=v22.11.6 \
    AARCH64_CRYPTOLIB_TAG=2445f0e

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
  software-properties-common \
  dirmngr \
  gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture arm64 && \
  apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com focal main universe" && \
  apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com focal-updates main universe"

RUN apt-get update --fix-missing

# Install fails if done together with other packages
RUN apt-get install -o APT::Immediate-Configure=false -y \
  libc6:arm64

RUN apt-get install -y \
  crossbuild-essential-arm64 \
  libcli-dev:arm64 \
  libconfig-dev:arm64 \
  libcunit1-dev:arm64 \
  libpcap-dev:arm64 \
  libssl-dev:arm64 \
  libstdc++-10-dev:arm64 \
  pkg-config-aarch64-linux-gnu \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  gcc-10 \
  git \
  iproute2 \
  kmod \
  libtool \
  meson \
  net-tools \
  ninja-build \
  python3-pip \
  sudo

RUN pip3 install \
  pyelftools

# '-moutline-atomics' removed to fix clang build
RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    sed 's/-moutline-atomics//g' -i config/arm/meson.build && \
    meson setup build --cross-file config/arm/arm64_armv8_linux_gcc && \
    cd build && \
    meson configure -Dlibdir=lib/aarch64-linux-gnu && \
    meson configure -Dprefix=/usr && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    git checkout ${AARCH64_CRYPTOLIB_TAG} && \
    make OPT=big CROSS=aarch64-linux-gnu- && \
    cd -
