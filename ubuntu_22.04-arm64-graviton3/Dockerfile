FROM ubuntu:22.04

ENV DPDK_VERSION=v22.11.6 \
    IPSEC_MB_VERSION=SECLIB-IPSEC-2022.12.13 \
    XDP_VERSION=v1.2.3 \
    AARCH64_CRYPTOLIB_TAG=2445f0e \
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
  git \
  iproute2 \
  kmod \
  libbpf-dev \
  libcli-dev \
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
  nasm \
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
        https://github.com/microsoft/onnxruntime/releases/download/v${ONNX_VERSION}/onnxruntime-linux-aarch64-${ONNX_VERSION}.tgz | \
        tar zx --strip-components=1 --wildcards "*/include" "*/lib" && \
    ldconfig

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build && \
    cd build && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    git checkout ${AARCH64_CRYPTOLIB_TAG} && \
    make OPT=big && \
    cd -

RUN cd $HOME && \
    git clone https://git.gitlab.arm.com/arm-reference-solutions/ipsec-mb.git --branch ${IPSEC_MB_VERSION} --depth 1 ./ipsec-mb && \
    cd ipsec-mb && \
    make -j $(nproc) && \
    make install && \
    cd $HOME && \
    rm -r ./ipsec-mb

RUN cd $HOME && \
    git clone --recurse-submodules https://github.com/xdp-project/xdp-tools.git --branch ${XDP_VERSION} --depth 1 ./xdp && \
    cd xdp && \
    ./configure && \
    C_INCLUDE_PATH=/usr/include/aarch64-linux-gnu/ make && \
    make install && \
    ldconfig /usr/local/lib/ && \
    cd $HOME && \
    rm -r ./xdp
