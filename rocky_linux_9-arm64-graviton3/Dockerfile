FROM rockylinux:9

ENV DPDK_VERSION=v22.11.6 \
    AARCH64_CRYPTOLIB_TAG=2445f0e

RUN dnf install -y 'dnf-command(config-manager)'
RUN dnf config-manager --enable crb

RUN yum update -y

RUN yum install -y \
	https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm

RUN yum install -y \
	autoconf \
	automake \
	clang \
	CUnit-devel \
	diffutils \
	gcc \
	gcc-c++ \
	gcc-toolset-12-libatomic-devel \
	git-core \
	glibc-static \
	kmod \
	libatomic \
	libconfig-devel \
	libibverbs-devel \
	libpcap-devel \
	libtool \
	make \
	meson \
	numactl-devel \
	net-tools \
	ninja-build \
	openssl-devel \
	pkgconfig \
	python3-pip \
	procps \
	sudo \
	zlib-devel

RUN pip3 install \
	pyelftools

RUN cd $HOME && \
    git clone https://github.com/DPDK/dpdk-stable.git --branch ${DPDK_VERSION} --depth 1 ./dpdk && \
    cd dpdk && \
    meson setup build && \
    cd build && \
    meson configure -Ddisable_apps=* && \
    meson configure -Dtests=false && \
    meson configure -Denable_drivers=crypto/*,dma/*,net/pcap && \
    ninja install && \
    ldconfig && \
    cd $HOME && \
    rm -r ./dpdk

RUN cd $HOME && \
    git clone https://github.com/ARM-software/AArch64cryptolib --depth 1 ./aarch64cryptolib && \
    cd aarch64cryptolib && \
    git checkout ${AARCH64_CRYPTOLIB_TAG} && \
    make OPT=big && \
    cd -
