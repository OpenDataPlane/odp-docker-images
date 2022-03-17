FROM ubuntu:22.04

ENV DPDK_VERSION=v20.11.4 \
  IPSEC_MB_VERSION=v1.1

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
  nasm \
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
    git clone https://github.com/intel/intel-ipsec-mb.git --branch ${IPSEC_MB_VERSION} --depth 1 ./ipsec-mb && \
    cd ipsec-mb && \
    make -j $(nproc) && \
    make install && \
    cd -

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson build && \
    cd build && \
    meson configure -Dmachine=default && \
    ninja && \
    ninja install && \
    cd -
