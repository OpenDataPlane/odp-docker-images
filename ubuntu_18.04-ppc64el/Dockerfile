FROM ubuntu:18.04

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture ppc64el && \
 apt-add-repository -y "deb [arch=ppc64el] http://ports.ubuntu.com bionic main universe" && \
 apt-add-repository -y "deb [arch=ppc64el] http://ports.ubuntu.com bionic-updates main universe"

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  crossbuild-essential-ppc64el \
  libconfig-dev:ppc64el \
  libcunit1-dev:ppc64el \
  libdpdk-dev:ppc64el \
  libpcap-dev:ppc64el \
  libssl-dev:ppc64el \
  libstdc++-7-dev:ppc64el \
  pkg-config-powerpc64le-linux-gnu \
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
