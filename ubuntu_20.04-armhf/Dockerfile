FROM ubuntu:20.04

ENV DPDK_VERSION=v22.11.6

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
  software-properties-common \
  dirmngr \
  gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture armhf && \
  apt-add-repository -y "deb [arch=armhf] http://ports.ubuntu.com focal main universe" && \
  apt-add-repository -y "deb [arch=armhf] http://ports.ubuntu.com focal-updates main universe"

RUN apt-get update --fix-missing

# Install fails if done together with other packages
RUN apt-get install -o APT::Immediate-Configure=false -y libc6:armhf

RUN apt-get install -y \
  crossbuild-essential-armhf \
  libcli-dev:armhf \
  libconfig-dev:armhf \
  libcunit1-dev:armhf \
  libpcap-dev:armhf \
  libssl-dev:armhf \
  libstdc++-10-dev:armhf \
  pkg-config-arm-linux-gnueabihf \
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

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build --cross-file config/arm/arm32_armv8_linux_gcc && \
    cd build && \
    meson configure -Dlibdir=lib/arm-linux-gnueabihf && \
    meson configure -Dprefix=/usr && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk
