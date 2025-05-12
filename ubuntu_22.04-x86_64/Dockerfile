FROM ubuntu:22.04

ENV DPDK_VERSION=v22.11.6 \
    XDP_VERSION=v1.2.3 \
    ONNX_VERSION=1.16.3

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
      software-properties-common \
      dirmngr \
      gnupg-agent

# Required for gcc-13
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  gcc-10 \
  gcc-11 \
  gcc-12 \
  gcc-13 \
  gcc-multilib \
  git \
  iproute2 \
  kmod \
  libbpf-dev \
  libconfig-dev \
  libcunit1-dev \
  libpcap-dev \
  libssl-dev \
  libstdc++-10-dev \
  libstdc++-11-dev \
  libstdc++-12-dev \
  libstdc++-13-dev \
  libtool \
  llvm-dev \
  meson \
  net-tools \
  ninja-build \
  python3-pip \
  sudo \
  wget

RUN pip3 install \
  numpy \
  onnx \
  pyelftools

RUN cd /usr/local && \
    wget -O - \
        https://github.com/microsoft/onnxruntime/releases/download/v${ONNX_VERSION}/onnxruntime-linux-x64-${ONNX_VERSION}.tgz | \
        tar zx --strip-components=1 --wildcards "*/include" "*/lib" && \
    ldconfig

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build && \
    cd build && \
    meson configure -Dplatform=generic && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk

RUN cd $HOME && \
    git clone --recurse-submodules https://github.com/xdp-project/xdp-tools.git --branch ${XDP_VERSION} --depth 1 ./xdp && \
    cd xdp && \
    ./configure && \
    make && \
    make install && \
    ldconfig /usr/local/lib/ && \
    cd $HOME && \
    rm -r ./xdp
