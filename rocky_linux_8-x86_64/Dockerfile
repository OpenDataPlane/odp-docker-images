FROM rockylinux:8.5

ENV DPDK_VERSION=v19.11.11 \
    RTE_ARCH=x86_64 \
    RTE_TARGET=x86_64-native-linuxapp-gcc

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
	gcc-toolset-11-libatomic-devel \
	git-core \
	kmod \
	libatomic \
	libconfig-devel \
	libpcap-devel \
	libtool \
	make \
	numactl-devel \
	net-tools \
	openssl-devel \
	pkgconfig \
	procps \
	sudo

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
    cd $HOME && \
    rm -r ./dpdk
