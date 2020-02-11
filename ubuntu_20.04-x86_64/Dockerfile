FROM ubuntu:20.04

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  asciidoctor \
  autoconf \
  automake \
  ccache \
  clang \
  dpdk-dev \
  gcc \
  git \
  graphviz \
  iproute2 \
  kmod \
  libconfig-dev \
  libcunit1-dev \
  libibverbs-dev \
  libnuma-dev \
  libpcap-dev \
  libssl-dev \
  libtool \
  mscgen \
  net-tools \
  python-pip \
  ruby-dev \
  sudo \
  xsltproc && \
pip install coverage
