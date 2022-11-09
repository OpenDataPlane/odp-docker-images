FROM ubuntu:18.04

ENV DPDK_VERSION=v19.11.13 \
	RTE_ARCH=i686 \
	RTE_TARGET=i686-native-linuxapp-gcc

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64,i386] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture i386

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  libcli-dev:i386 \
  libconfig-dev:i386 \
  libcunit1-dev:i386 \
  libpcap-dev:i386 \
  libssl-dev:i386 \
  lib32stdc++-7-dev \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  gcc-multilib \
  g++-multilib \
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
    make -j $(nproc) install T=${RTE_TARGET} DESTDIR=/usr EXTRA_CFLAGS="-fPIC" && \
    cd $HOME && \
    rm -r ./dpdk
