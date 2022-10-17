FROM ubuntu:20.04

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
  libdpdk-dev:armhf \
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
  libnuma-dev \
  libtool \
  net-tools \
  sudo
