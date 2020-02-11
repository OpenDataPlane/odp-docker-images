FROM ubuntu:18.04

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64,i386] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture i386

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  libconfig-dev:i386 \
  libcunit1-dev:i386 \
  libdpdk-dev:i386 \
  libpcap-dev:i386 \
  libssl-dev:i386 \
  lib32stdc++-7-dev \
  asciidoctor \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  gcc-multilib \
  g++-multilib \
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
