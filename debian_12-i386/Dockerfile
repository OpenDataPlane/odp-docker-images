FROM debian:12

ENV DPDK_VERSION=v23.11.4

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
  software-properties-common \
	dirmngr \
	gnupg-agent

RUN rm -f /etc/apt/sources.list.d/debian.sources

RUN [ -f /etc/apt/sources.list ] || echo "deb http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware" > /etc/apt/sources.list

RUN dpkg --add-architecture i386

RUN sed -e 's/^deb /deb [arch=amd64,i386] /g' /etc/apt/sources.list -i

RUN tee /etc/apt/sources.list <<EOF
deb [arch=amd64,i386] http://deb.debian.org/debian bookworm main contrib non-free non-free-firmware
deb [arch=amd64,i386] http://deb.debian.org/debian bookworm-updates main contrib non-free non-free-firmware
deb [arch=amd64,i386] http://security.debian.org/debian-security bookworm-security main contrib non-free non-free-firmware
EOF

RUN apt-get update --fix-missing

RUN apt-get install -y --allow-downgrades perl-base=5.36.0-7+deb12u1

RUN apt-get install -yy \
  libcli-dev:i386 \
  libconfig-dev:i386 \
  libcunit1-dev:i386 \
  liblzma5:i386 \
  libnuma-dev:i386 \
  libpcap-dev:i386 \
  libssl-dev:i386 \
  libsystemd0:i386 \
  libsystemd-dev:i386  \
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
  python3-pyelftools

RUN cd $HOME && \
  git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
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