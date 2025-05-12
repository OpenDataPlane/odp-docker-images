FROM rockylinux:8

ENV DPDK_VERSION=v22.11.6

RUN dnf install -y 'dnf-command(config-manager)'
RUN dnf config-manager --set-enabled powertools

RUN yum update -y

RUN yum install -y \
	https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

RUN yum install -y \
	autoconf \
	automake \
	clang \
	CUnit-devel \
	curl \
	diffutils \
	gcc \
	gcc-c++ \
	gcc-toolset-13-libatomic-devel \
	git-core \
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
