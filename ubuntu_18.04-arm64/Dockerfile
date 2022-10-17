FROM ubuntu:18.04

ENV DPDK_VERSION=v19.11.6 \
	RTE_ARCH=arm64 \
	RTE_TARGET=arm64-armv8a-linuxapp-gcc \
	CROSS_TOOLS=aarch64-linux-gnu-

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture arm64 && \
 apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com bionic main universe" && \
 apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com bionic-updates main universe"

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  crossbuild-essential-arm64 \
  libcli-dev:arm64 \
  libconfig-dev:arm64 \
  libcunit1-dev:arm64 \
  libpcap-dev:arm64 \
  libssl-dev:arm64 \
  libstdc++-7-dev:arm64 \
  pkg-config-aarch64-linux-gnu \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  git \
  iproute2 \
  kmod \
  libnuma-dev \
  libtool \
  net-tools \
  sudo

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
    make -j $(nproc) install CROSS=${CROSS_TOOLS} T=${RTE_TARGET} DESTDIR=/usr EXTRA_CFLAGS="-fPIC" && \
    cd $HOME && \
    rm -r ./dpdk

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    make CC=aarch64-linux-gnu-gcc && \
    cd -
