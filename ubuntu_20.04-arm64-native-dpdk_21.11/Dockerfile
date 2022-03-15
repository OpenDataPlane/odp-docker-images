FROM ubuntu:20.04

ENV DPDK_VERSION=v21.11

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
  libcli-dev \
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
pip3 install \
  coverage \
  pyelftools

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson build && \
    cd build && \
    ninja && \
    ninja install && \
    cd -

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    make && \
    cd -
