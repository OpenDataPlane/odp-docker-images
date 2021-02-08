FROM centos:7

ENV DPDK_VERSION=v19.11.5 \
    RTE_ARCH=x86_64 \
    RTE_TARGET=x86_64-native-linuxapp-gcc \
    CUNIT_VERSION=2.1-3

RUN yum update -y

RUN yum install -y \
	https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

RUN yum install -y \
	autoconf \
	automake \
	bzip2 \
	clang \
	curl \
	doxygen \
	gcc \
	gcc-c++ \
	git-core \
	graphviz \
	kmod \
	libatomic \
	libcli-devel \
	libconfig-devel \
	libpcap-devel \
	libtool \
	make \
	numactl-devel \
	net-tools \
	openssl-devel \
	pkgconfig \
	sudo


RUN cd $HOME && \
    curl -sSOL http://sourceforge.net/projects/cunit/files/CUnit/${CUNIT_VERSION}/CUnit-${CUNIT_VERSION}.tar.bz2 && \
    tar -jxf *.bz2 && \
    cd CUnit* && \
    ./bootstrap && \
    ./configure && \
    make && \
    make install && \
    cd -

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
    cd -
