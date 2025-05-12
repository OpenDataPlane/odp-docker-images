FROM ubuntu:24.04

ENV DPDK_VERSION=v22.11.6

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
  software-properties-common \
  dirmngr \
  gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture ppc64el

RUN rm -f /etc/apt/sources.list.d/ubuntu.sources

RUN cat <<EOF > /etc/apt/sources.list.d/ubuntu.sources
# amd64 repositories (use archive.ubuntu.com and security.ubuntu.com)
Types: deb
URIs: http://archive.ubuntu.com/ubuntu/
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Architectures: amd64
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: http://security.ubuntu.com/ubuntu/
Suites: noble-security
Components: main restricted universe multiverse
Architectures: amd64
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
EOF

RUN cat <<EOF > /etc/apt/sources.list.d/ubuntu_ppc64el.sources
# ppc64el repositories (use ports.ubuntu.com)
Types: deb
URIs: http://ports.ubuntu.com/ubuntu-ports/
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Architectures: ppc64el
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: http://ports.ubuntu.com/ubuntu-ports/
Suites: noble-security
Components: main restricted universe multiverse
Architectures: ppc64el
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
EOF

RUN apt-get update --fix-missing

RUN apt-get install -y \
  crossbuild-essential-ppc64el \
  libc6:ppc64el \
  libcli-dev:ppc64el \
  libconfig-dev:ppc64el \
  libcunit1-dev:ppc64el \
  libpcap-dev:ppc64el \
  libssl-dev:ppc64el \
  libstdc++-10-dev:ppc64el \
  autoconf \
  automake \
  ccache \
  clang \
  gcc \
  gcc-10 \
  git \
  iproute2 \
  kmod \
  libtool \
  meson \
  net-tools \
  ninja-build \
  python3-pip \
  python3-pyelftools \
  sudo

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build --cross-file config/ppc/ppc64le-power8-linux-gcc-ubuntu && \
    cd build && \
    meson configure -Dlibdir=lib/powerpc64le-linux-gnu && \
    meson configure -Dprefix=/usr && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk
