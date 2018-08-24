FROM ubuntu:18.04

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  asciidoctor \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  graphviz \
  kmod \
  libconfig-dev \
  libcunit1-dev \
  libnuma-dev \
  libpcap-dev \
  libssl-dev \
  libtool \
  net-tools \
  mscgen \
  ruby-dev \
  xsltproc \
  git \
  iproute2 \
  libdpdk-dev \
  dpdk \
  dpdk-dev \
  python-pip && \
pip install coverage
