FROM ubuntu:20.04

ARG COVERITY_TOKEN

ENV COVERITY_PROJECT=ODP-DPDK

ENV DPDK_VERSION=v19.11.6 \
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
  curl \
  gcc \
  gcc-10 \
  git \
  libcli-dev \
  libconfig-dev \
  libcunit1-dev \
  libnuma-dev \
  libpcap-dev \
  libssl-dev \
  libtool \
  libstdc++-10-dev \
  make \
  sudo

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    make config T=${RTE_TARGET} O=${RTE_TARGET} && \
    cd ${RTE_TARGET} && \
    sed -ri 's,(CONFIG_RTE_MACHINE=).*,\1"default",' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_PCAP=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_OPENSSL=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_EAL_IGB_UIO=).*,\1n,' .config && \
    sed -ri 's,(CONFIG_RTE_KNI_KMOD=).*,\1n,' .config && \
    cd .. && \
    make -j $(nproc) install T=${RTE_TARGET} DESTDIR=/usr EXTRA_CFLAGS="-fPIC" && \
    cd $HOME && \
    rm -r ./dpdk

RUN curl -d "token=${COVERITY_TOKEN}&project=${COVERITY_PROJECT}" -o /coverity_tool.tgz https://scan.coverity.com/download/linux64 && \
  mkdir /coverity_tool && \
  tar xf /coverity_tool.tgz --strip 1 -C /coverity_tool

ENV PATH="${PATH}:/coverity_tool/bin"
