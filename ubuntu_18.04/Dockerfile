FROM ubuntu:18.04

ENV DPDK_VERSION=17.11 \
	RTE_ARCH=x86_64 \
	RTE_TARGET=x86_64-native-linuxapp-gcc

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
  graphviz \
  kmod \
  libconfig-dev \
  libcunit1-dev \
  libnuma-dev \
  libpcap-dev \
  libssl-dev \
  libtool \
  net-tools \
  mscgen \
  ruby-dev \
  sudo \
  xsltproc \
  git \
  iproute2 \
  libibverbs-dev \
  python-pip && \
pip install coverage

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    make config T=x86_64-native-linuxapp-gcc O=x86_64-native-linuxapp-gcc && \
    cd x86_64-native-linuxapp-gcc/ && \
    sed -ri 's,(CONFIG_RTE_MACHINE=).*,\1"default",' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_PCAP=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_LIBRTE_PMD_OPENSSL=).*,\1y,' .config && \
    sed -ri 's,(CONFIG_RTE_EAL_IGB_UIO=).*,\1n,' .config && \
    sed -ri 's,(CONFIG_RTE_KNI_KMOD=).*,\1n,' .config && \
    cd .. && \
    make -j $(nproc) install T=x86_64-native-linuxapp-gcc DESTDIR=/usr EXTRA_CFLAGS="-fPIC" && \
    cd -
