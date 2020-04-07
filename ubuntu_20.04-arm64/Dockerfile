FROM ubuntu:20.04

ENV DPDK_VERSION=18.11 \
	RTE_ARCH=arm64 \
	RTE_TARGET=arm64-armv8a-linuxapp-gcc

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
  software-properties-common \
  dirmngr \
  gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture arm64 && \
  apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com focal main universe" && \
  apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com focal-updates main universe"

RUN apt-get update --fix-missing

# Install fails if done together with other packages
RUN apt-get install -o APT::Immediate-Configure=false -y \
  libc6:arm64

RUN apt-get install -y \
  crossbuild-essential-arm64 \
  libconfig-dev:arm64 \
  libcunit1-dev:arm64 \
  libpcap-dev:arm64 \
  libssl-dev:arm64 \
  libstdc++-9-dev:arm64 \
  pkg-config-aarch64-linux-gnu \
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
  libnuma-dev \
  libtool \
  mscgen \
  net-tools \
  python3-pip \
  ruby-dev \
  sudo \
  xsltproc && \
pip3 install coverage

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    make config T=${RTE_TARGET} O=${RTE_TARGET} && \
    cd ${RTE_TARGET} && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_PCAP=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_OPENSSL=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_EAL_IGB_UIO=).*,\1n,' .config && \
    sed -ri 's,(CONFIG_RTE_KNI_KMOD=).*,\1n,' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_VHOST_NUMA=).*,\1n,' .config && \
    sed -ri 's,(CONFIG_RTE_EAL_NUMA_AWARE_HUGEPAGES=).*,\1n,' .config && \
    cd .. && \
    make -j $(nproc) install CROSS=aarch64-linux-gnu- T=${RTE_TARGET} DESTDIR=/usr EXTRA_CFLAGS="-fPIC" && \
    cd -
