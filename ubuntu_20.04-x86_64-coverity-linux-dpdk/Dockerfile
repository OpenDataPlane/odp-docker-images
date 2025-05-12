FROM ubuntu:20.04

ARG COVERITY_TOKEN

ENV COVERITY_PROJECT=ODP-DPDK

ENV DPDK_VERSION=v22.11.6

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
  git \
  libcli-dev \
  libconfig-dev \
  libcunit1-dev \
  libnuma-dev \
  libpcap-dev \
  libssl-dev \
  libtool \
  make \
  meson \
  net-tools \
  ninja-build \
  python3-pip \
  sudo

RUN pip3 install \
  pyelftools

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build && \
    cd build && \
    meson configure -Dplatform=generic && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk

RUN curl -d "token=${COVERITY_TOKEN}&project=${COVERITY_PROJECT}" -o /coverity_tool.tgz https://scan.coverity.com/download/linux64 && \
  mkdir /coverity_tool && \
  tar xf /coverity_tool.tgz --strip 1 -C /coverity_tool

ENV PATH="${PATH}:/coverity_tool/bin"
