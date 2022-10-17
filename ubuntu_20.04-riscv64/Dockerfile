FROM ubuntu:20.04

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
  software-properties-common \
  dirmngr \
  gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture riscv64 && \
  apt-add-repository -y "deb [arch=riscv64] http://ports.ubuntu.com focal main universe" && \
  apt-add-repository -y "deb [arch=riscv64] http://ports.ubuntu.com focal-updates main universe"

RUN apt-get update --fix-missing

# Install fails if done together with other packages
RUN apt-get install -o APT::Immediate-Configure=false -y \
  libc6:riscv64

RUN apt-get install -y \
  crossbuild-essential-riscv64 \
  libcli-dev:riscv64 \
  libconfig-dev:riscv64 \
  libcunit1-dev:riscv64 \
  libpcap-dev:riscv64 \
  libssl-dev:riscv64 \
  libstdc++-10-dev:riscv64 \
  pkg-config-riscv64-linux-gnu \
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

