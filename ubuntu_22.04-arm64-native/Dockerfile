FROM ubuntu:22.04

ENV DPDK_VERSION=v20.11.4 \
  XDP_VERSION=v1.2.3

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
  gcc-11 \
  gcc-12 \
  git \
  graphviz \
  iproute2 \
  kmod \
  libbpf-dev \
  libcli-dev \
  libconfig-dev \
  libcunit1-dev \
  libibverbs-dev \
  libnuma-dev \
  libpcap-dev \
  libssl-dev \
  libstdc++-10-dev \
  libstdc++-11-dev \
  libstdc++-12-dev \
  libtool \
  llvm-dev \
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

RUN cd $HOME && \
    git clone --recurse-submodules https://github.com/xdp-project/xdp-tools.git --branch ${XDP_VERSION} --depth 1 ./xdp && \
    cd xdp && \
    ./configure && \
    C_INCLUDE_PATH=/usr/include/aarch64-linux-gnu/ make && \
    make install && \
    ldconfig /usr/local/lib/ && \
    cd -
