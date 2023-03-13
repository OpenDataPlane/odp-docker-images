FROM ubuntu:22.04

ENV DPDK_VERSION=v22.11.1 \
    OPENSSL_VERSION=OpenSSL_1_1_1o \
    XDP_VERSION=v1.2.3

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  git \
  iproute2 \
  kmod \
  libbpf-dev \
  libcli-dev \
  libconfig-dev \
  libcunit1-dev \
  libpcap-dev \
  libstdc++-10-dev \
  libtool \
  llvm-dev \
  meson \
  net-tools \
  ninja-build \
  python3-pip \
  sudo

RUN pip3 install \
  pyelftools

RUN cd $HOME && \
    git clone https://github.com/openssl/openssl.git --branch ${OPENSSL_VERSION} --depth 1 ./openssl && \
    cd openssl && \
    ./config && \
    make -j $(nproc) && \
    make install && \
    cd $HOME && \
    rm -r ./openssl

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build && \
    cd build && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    ninja && \
    ninja install && \
    cd $HOME && \
    rm -r ./dpdk

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
    cd $HOME && \
    rm -r ./xdp
