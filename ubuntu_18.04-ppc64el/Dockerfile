FROM ubuntu:18.04

ENV DPDK_VERSION=v19.11.13 \
	RTE_ARCH=ppc_64 \
	RTE_TARGET=ppc_64-power8-linuxapp-gcc \
	CROSS_TOOLS=powerpc64le-linux-gnu-

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture ppc64el && \
 apt-add-repository -y "deb [arch=ppc64el] http://ports.ubuntu.com bionic main universe" && \
 apt-add-repository -y "deb [arch=ppc64el] http://ports.ubuntu.com bionic-updates main universe"

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  crossbuild-essential-ppc64el \
  libcli-dev:ppc64el \
  libconfig-dev:ppc64el \
  libcunit1-dev:ppc64el \
  libpcap-dev:ppc64el \
  libssl-dev:ppc64el \
  libstdc++-7-dev:ppc64el \
  pkg-config-powerpc64le-linux-gnu \
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
