FROM ubuntu:20.04

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
  libdpdk-dev:arm64 \
  libpcap-dev:arm64 \
  libssl-dev:arm64 \
  libstdc++-10-dev:arm64 \
  pkg-config-aarch64-linux-gnu \
  asciidoctor \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  gcc-10 \
  git \
  graphviz \
  iproute2 \
  kmod \
  libnuma-dev \
  libtool \
  mscgen \
  net-tools \
  python3-pip \
  ruby-dev \
  sudo \
  xsltproc && \
pip3 install coverage

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    make CC=aarch64-linux-gnu-gcc && \
    cd -
