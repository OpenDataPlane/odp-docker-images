FROM ubuntu:16.04

RUN apt-get update --fix-missing

RUN apt-get install -yy --no-install-recommends \
	software-properties-common

RUN sed -e 's/^deb http/deb [arch=amd64,i386] http/g' /etc/apt/sources.list -i

RUN add-apt-repository -y ppa:lumag/odp-xenial

RUN dpkg --add-architecture i386 && \
 dpkg --add-architecture armhf && \
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
	net-tools \
	mscgen \
	graphviz \
	python-pip \
	xsltproc \
	iproute2 \
	curl \
	ccache \
	crossbuild-essential-arm64 \
	pkg-config-aarch64-linux-gnu \
	crossbuild-essential-armhf \
	pkg-config-arm-linux-gnueabihf \
	crossbuild-essential-powerpc \
	pkg-config-powerpc-linux-gnu \
	lib32stdc++-5-dev \
	libstdc++-5-dev:arm64 \
	libstdc++-5-dev:armhf \
	libstdc++-5-dev:powerpc \
	libdpdk-dev:amd64 \
	libdpdk-dev:i386 \
	libdpdk-dev:armhf \
	libdpdk-dev:arm64 \
	libcunit1-dev:amd64 \
	libcunit1-dev:i386 \
	libcunit1-dev:armhf \
	libcunit1-dev:arm64 \
	libcunit1-dev:powerpc \
	libpcap0.8-dev:amd64 \
	libpcap0.8-dev:i386 \
	libpcap0.8-dev:armhf \
	libpcap0.8-dev:arm64 \
	libpcap0.8-dev:powerpc \
	libssl-dev:amd64 \
	libssl-dev:i386 \
	libssl-dev:armhf \
	libssl-dev:arm64 \
	libssl-dev:powerpc \
	libconfig-dev:amd64 \
	libconfig-dev:i386 \
	libconfig-dev:armhf \
	libconfig-dev:arm64 \
	libconfig-dev:powerpc \
	kmod \
	clang \
	build-essential \
	sudo

RUN pip install coverage
