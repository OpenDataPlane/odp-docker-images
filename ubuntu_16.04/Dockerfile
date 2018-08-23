FROM ubuntu:16.04

RUN apt-get update --fix-missing

RUN apt-get install -yy --no-install-recommends \
	software-properties-common

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN add-apt-repository -y ppa:lumag/odp-xenial

RUN dpkg --add-architecture armhf && \
 dpkg --add-architecture arm64 && \
 dpkg --add-architecture powerpc && \
 apt-add-repository -y "deb [arch=armhf,arm64,powerpc] http://ports.ubuntu.com xenial main universe" && \
 apt-add-repository -y "deb [arch=armhf,arm64,powerpc] http://ports.ubuntu.com xenial-updates main universe"

RUN apt-get update --fix-missing

RUN apt-get install -yy --no-install-recommends \
	git-core \
	autoconf \
	automake \
	libtool \
	pkg-config \
	asciidoctor \
	doxygen \
	mscgen \
	graphviz \
	python-pip \
	xsltproc \
	iproute2 \
	ccache \
	crossbuild-essential-arm64 \
	crossbuild-essential-armhf \
	crossbuild-essential-powerpc \
	libdpdk-dev \
	libdpdk-dev:armhf \
	libdpdk-dev:arm64 \
	libcunit1-dev \
	libcunit1-dev:armhf \
	libcunit1-dev:arm64 \
	libcunit1-dev:powerpc \
	libpcap0.8-dev \
	libpcap0.8-dev:armhf \
	libpcap0.8-dev:arm64 \
	libpcap0.8-dev:powerpc \
	libssl-dev \
	libssl-dev:armhf \
	libssl-dev:arm64 \
	libssl-dev:powerpc \
	libconfig-dev \
	libconfig-dev:armhf \
	libconfig-dev:arm64 \
	libconfig-dev:powerpc \
	clang \
	build-essential

RUN pip install coverage
