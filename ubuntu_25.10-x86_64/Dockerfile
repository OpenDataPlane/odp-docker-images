FROM ubuntu:25.10

ENV DPDK_VERSION=v23.11.4 \
    XDP_VERSION=v1.5.8 \
    ONNX_VERSION=1.16.3

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
  gcc-15 \
  gcc-multilib \
  git \
  graphviz \
  iproute2 \
  kmod \
  libbpf-dev \
  libconfig-dev \
  libcunit1-dev \
  libnuma-dev \
  libpcap-dev \
  libssl-dev \
  libstdc++-15-dev \
  libsystemd-dev \
  libtool \
  llvm-dev \
  meson \
  mscgen \
  net-tools \
  ninja-build \
  python3-pip \
  python3-pyelftools \
  sudo \
  wget

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
