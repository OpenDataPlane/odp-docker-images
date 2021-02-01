FROM ubuntu:18.04

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture armhf && \
 apt-add-repository -y "deb [arch=armhf] http://ports.ubuntu.com bionic main universe" && \
 apt-add-repository -y "deb [arch=armhf] http://ports.ubuntu.com bionic-updates main universe"

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  crossbuild-essential-armhf \
  libcli-dev:armhf \
  libconfig-dev:armhf \
  libcunit1-dev:armhf \
  libpcap-dev:armhf \
  libssl-dev:armhf \
  libstdc++-7-dev:armhf \
  pkg-config-arm-linux-gnueabihf \
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
