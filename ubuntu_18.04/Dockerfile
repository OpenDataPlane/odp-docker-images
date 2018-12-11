FROM ubuntu:18.04

RUN apt-get update

RUN apt-get install -yy --no-install-recommends \
        software-properties-common \
	dirmngr \
	gnupg-agent

RUN sed -e 's/^deb http/deb [arch=amd64,i386] http/g' /etc/apt/sources.list -i
RUN echo deb http://ppa.launchpad.net/lumag/odp-xenial/ubuntu xenial main > /etc/apt/sources.list.d/lumag-ppa.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 41E0C15904CF4B2F

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
  libdpdk-dev:amd64 \
  libibverbs-dev \
  python-pip && \
pip install coverage
