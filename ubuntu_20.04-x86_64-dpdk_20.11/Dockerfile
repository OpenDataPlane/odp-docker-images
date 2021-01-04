FROM ubuntu:20.04

ENV DPDK_VERSION=v20.11

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
  gcc \
  gcc-10 \
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
  libstdc++-10-dev \
  libtool \
  meson \
  mscgen \
  net-tools \
  ninja-build \
  python3-pip \
  ruby-dev \
  sudo \
  xsltproc && \
pip3 install coverage

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson build && \
    cd build && \
    meson configure -Dmachine=default && \
    ninja && \
    ninja install && \
    cd -
