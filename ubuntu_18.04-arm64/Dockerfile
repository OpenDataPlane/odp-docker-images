FROM ubuntu:18.04

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
  libconfig-dev:arm64 \
  libcunit1-dev:arm64 \
  libdpdk-dev:arm64 \
  libpcap-dev:arm64 \
  libssl-dev:arm64 \
  libstdc++-7-dev:arm64 \
  pkg-config-aarch64-linux-gnu \
  asciidoctor \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  git \
  graphviz \
  iproute2 \
  kmod \
  libnuma-dev \
  libtool \
  mscgen \
  net-tools \
  python-pip \
  ruby-dev \
  sudo \
  xsltproc && \
pip install coverage
