FROM ubuntu:20.04

ENV DPDK_VERSION=v19.11.14 \
    IPSEC_MB_VERSION=v0.55 \
    RTE_ARCH=x86_64 \
    RTE_TARGET=x86_64-native-linuxapp-gcc

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
  gcc-10 \
  git \
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
  make \
  nasm \
  net-tools \
  sudo

RUN cd $HOME && \
    git clone https://github.com/intel/intel-ipsec-mb.git --branch ${IPSEC_MB_VERSION} --depth 1 ./ipsec-mb && \
    cd ipsec-mb && \
    make -j $(nproc) && \
    make install && \
    cd $HOME && \
    rm -r ./ipsec-mb

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    make config T=${RTE_TARGET} O=${RTE_TARGET} && \
    cd ${RTE_TARGET} && \
    sed -ri 's,(CONFIG_RTE_MACHINE=).*,\1"default",' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_AESNI_GCM=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_AESNI_MB=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_PCAP=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_OPENSSL=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_EAL_IGB_UIO=).*,\1n,' .config && \
    sed -ri 's,(CONFIG_RTE_KNI_KMOD=).*,\1n,' .config && \
    cd .. && \
    make -j $(nproc) install T=${RTE_TARGET} DESTDIR=/usr EXTRA_CFLAGS="-fPIC" && \
    cd $HOME && \
    rm -r ./dpdk
