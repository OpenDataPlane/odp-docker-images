FROM ubuntu:18.04

ENV DPDK_VERSION=v22.11.1

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture arm64 && \
 apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com bionic main universe" && \
 apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com bionic-updates main universe"

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  crossbuild-essential-arm64 \
  libcli-dev:arm64 \
  libconfig-dev:arm64 \
  libcunit1-dev:arm64 \
  libpcap-dev:arm64 \
  libssl-dev:arm64 \
  libstdc++-7-dev:arm64 \
  pkg-config-aarch64-linux-gnu \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  git \
  iproute2 \
  kmod \
  libtool \
  net-tools \
  ninja-build \
  python3-pip \
  sudo

RUN pip3 install \
  meson \
  pyelftools

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build --cross-file config/arm/arm64_armv8_linux_gcc && \
    cd build && \
    meson configure -Ddisable_drivers=event/cnxk && \
    meson configure -Dlibdir=lib/aarch64-linux-gnu && \
    meson configure -Dprefix=/usr && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    ninja && \
    ninja install && \
    cd $HOME && \
    rm -r ./dpdk

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    make CC=aarch64-linux-gnu-gcc && \
    cd -
