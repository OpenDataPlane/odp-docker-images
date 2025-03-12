FROM i386/debian:12

ENV DPDK_VERSION=v22.11.6

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN rm -f /etc/apt/sources.list.d/debian.sources

RUN [ -f /etc/apt/sources.list ] || echo "deb http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware" > /etc/apt/sources.list

RUN dpkg --add-architecture i386

RUN sed -e 's/^deb /deb [arch=amd64,i386] /g' /etc/apt/sources.list -i

RUN apt-get update --fix-missing

RUN apt-get install -yy \
  libcli-dev:i386 \
  libconfig-dev:i386 \
  libcunit1-dev:i386 \
  libpcap-dev:i386 \
  libssl-dev:i386 \
  g++-multilib \
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
  libtool \
  net-tools \
  ninja-build \
  python3-pip \
  sudo \
  meson \
  python3-pyelftools \
  libsystemd-dev

RUN cd $HOME && \
    git clone http://dpdk.org/git/dpdk-stable --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    PKG_CONFIG_LIBDIR=/usr/lib/i386-linux-gnu/pkgconfig \
    meson setup -Dc_args='-m32' -Dc_link_args='-m32' build && \
    cd build && \
    meson configure -Dlibdir=lib/i386-linux-gnu && \
    meson configure -Dmachine=default && \
    meson configure -Dprefix=/usr && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk
