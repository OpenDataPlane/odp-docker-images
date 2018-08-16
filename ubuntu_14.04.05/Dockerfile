FROM ubuntu:14.04.5

RUN apt-get update --fix-missing

RUN apt-get install -yy \
	software-properties-common \
        curl

RUN sed -e 's/^deb http/deb [arch=amd64] http/g' /etc/apt/sources.list -i

RUN dpkg --add-architecture armhf && \
 apt-add-repository -y "deb [arch=armhf] http://ports.ubuntu.com trusty main" && \
 apt-add-repository -y "deb [arch=armhf] http://ports.ubuntu.com trusty-updates main" && \
 dpkg --add-architecture arm64 && \
 apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com trusty main" && \
 apt-add-repository -y "deb [arch=arm64] http://ports.ubuntu.com trusty-updates main" && \
 dpkg --add-architecture powerpc && \
 apt-add-repository -y "deb [arch=powerpc] http://ports.ubuntu.com trusty main" && \
 apt-add-repository -y "deb [arch=powerpc] http://ports.ubuntu.com trusty-updates main"

RUN apt-get update --fix-missing

RUN apt-get install -yy \
adduser \
apt \
apt-utils \
autoconf \
automake \
autotools-dev \
base-files \
base-passwd \
bash \
binfmt-support \
binutils \
binutils-2.26 \
binutils-aarch64-linux-gnu \
binutils-arm-linux-gnueabihf \
binutils-powerpc-linux-gnu \
bsdutils \
build-essential \
busybox-initramfs \
bzip2 \
ca-certificates \
clang-3.9 \
clang-3.9-doc \
clang-3.9-examples \
console-setup \
coreutils \
cpio \
cpp \
cpp-4.8 \
cpp-4.8-aarch64-linux-gnu \
cpp-4.8-arm-linux-gnueabihf \
cpp-4.8-powerpc-linux-gnu \
cpp-aarch64-linux-gnu \
cpp-arm-linux-gnueabihf \
cpp-powerpc-linux-gnu \
cron \
dash \
debconf \
debconf-i18n \
debianutils \
dh-python \
diffutils \
dmsetup \
dpkg \
dpkg-dev \
e2fslibs:amd64 \
e2fsprogs \
eject \
fakeroot \
file \
findutils \
fontconfig \
fontconfig-config \
fonts-dejavu-core \
fonts-liberation \
g++ \
g++-4.8 \
g++-4.8-aarch64-linux-gnu \
g++-4.8-arm-linux-gnueabihf \
g++-4.8-multilib \
g++-4.8-multilib-arm-linux-gnueabihf \
g++-aarch64-linux-gnu \
gcc \
gcc-4.8 \
gcc-4.8-aarch64-linux-gnu \
gcc-4.8-aarch64-linux-gnu-base \
gcc-4.8-arm-linux-gnueabihf \
gcc-4.8-arm-linux-gnueabihf-base \
gcc-4.8-base:amd64 \
gcc-4.8-base:arm64 \
gcc-4.8-multilib \
gcc-4.8-multilib-arm-linux-gnueabihf \
gcc-4.8-multilib-powerpc-linux-gnu \
gcc-4.8-powerpc-linux-gnu \
gcc-4.8-powerpc-linux-gnu-base \
gcc-4.9-base:amd64 \
gcc-4.9-base:arm64 \
gcc-4.9-base:armhf \
gcc-4.9-base:powerpc \
gcc-aarch64-linux-gnu \
gcc-arm-linux-gnueabihf \
gcc-powerpc-linux-gnu \
gir1.2-glib-2.0 \
git \
git-man \
gnupg \
gpgv \
graphviz \
grep \
gzip \
hostname \
ifupdown \
init-system-helpers \
initramfs-tools \
initramfs-tools-bin \
initscripts \
insserv \
iproute2 \
iputils-ping \
isc-dhcp-client \
isc-dhcp-common \
iso-codes \
kbd \
keyboard-configuration \
klibc-utils \
kmod \
krb5-locales \
less \
lib32asan0 \
lib32atomic1 \
lib32gcc-4.8-dev \
lib32gcc1 \
lib32gomp1 \
lib32itm1 \
lib32quadmath0 \
lib32stdc++-4.8-dev \
lib32stdc++6 \
lib64asan0-powerpc-cross \
lib64atomic1-powerpc-cross \
lib64gcc-4.8-dev-powerpc-cross \
lib64gcc1-powerpc-cross \
lib64gomp1-powerpc-cross \
libacl1:amd64 \
libalgorithm-diff-perl \
libalgorithm-diff-xs-perl \
libalgorithm-merge-perl \
libapt-inst1.5:amd64 \
libapt-pkg4.12:amd64 \
libarchive-extract-perl \
libasan0:amd64 \
libasan0-armhf-cross \
libasan0-powerpc-cross \
libasn1-8-heimdal:amd64 \
libatomic1:amd64 \
libatomic1:arm64 \
libatomic1-arm64-cross \
libatomic1-armhf-cross \
libatomic1-powerpc-cross \
libattr1:amd64 \
libaudit-common \
libaudit1:amd64 \
libblkid1:amd64 \
libbsd0:amd64 \
libbz2-1.0:amd64 \
libc-bin \
libc-dev-bin \
libc6:amd64 \
libc6:arm64 \
libc6:armhf \
libc6:powerpc \
libc6-arm64-cross \
libc6-armel-armhf-cross \
libc6-armel-cross \
libc6-armhf-cross \
libc6-dev:amd64 \
libc6-dev:arm64 \
libc6-dev:armhf \
libc6-dev:powerpc \
libc6-dev-arm64-cross \
libc6-dev-armel-armhf-cross \
libc6-dev-armel-cross \
libc6-dev-armhf-cross \
libc6-dev-i386 \
libc6-dev-powerpc-cross \
libc6-dev-ppc64-powerpc-cross \
libc6-dev-x32 \
libc6-i386 \
libc6-powerpc-cross \
libc6-ppc64-powerpc-cross \
libc6-x32 \
libcairo2:amd64 \
libcap2:amd64 \
libcap2-bin \
libcdt5 \
libcgmanager0:amd64 \
libcgraph6 \
libclang-3.9-dev \
libclang-common-3.4-dev \
libclang-common-3.9-dev \
libclang1-3.4:amd64 \
libclang1-3.9:amd64 \
libcloog-isl4:amd64 \
libcloog-isl4:arm64 \
libcomerr2:amd64 \
libconfig-dev:arm64 \
libconfig-dev:armhf \
libconfig-dev:powerpc \
libconfig8-dev \
libconfig9:arm64 \
libconfig9:armhf \
libconfig9:powerpc \
libcurl3-gnutls:amd64 \
libdatrie1:amd64 \
libdb5.3:amd64 \
libdbus-1-3:amd64 \
libdbus-glib-1-2:amd64 \
libdebconfclient0:amd64 \
libdevmapper1.02.1:amd64 \
libdpkg-perl \
libdrm2:amd64 \
libedit2:amd64 \
libelf-dev:amd64 \
libelf1:amd64 \
liberror-perl \
libestr0 \
libexpat1:amd64 \
libfakeroot:amd64 \
libffi-dev:amd64 \
libffi6:amd64 \
libfile-fcntllock-perl \
libfontconfig1:amd64 \
libfreetype6:amd64 \
libfribidi0:amd64 \
libgcc-4.8-dev:amd64 \
libgcc-4.8-dev:arm64 \
libgcc-4.8-dev-arm64-cross \
libgcc-4.8-dev-armhf-cross \
libgcc-4.8-dev-powerpc-cross \
libgcc1:amd64 \
libgcc1:arm64 \
libgcc1:armhf \
libgcc1:powerpc \
libgcc1-arm64-cross \
libgcc1-armhf-cross \
libgcc1-powerpc-cross \
libgcrypt11:amd64 \
libgd3:amd64 \
libgdbm3:amd64 \
libgirepository-1.0-1 \
libglib2.0-0:amd64 \
libglib2.0-data \
libgmp10:amd64 \
libgmp10:arm64 \
libgnutls-openssl27:amd64 \
libgnutls26:amd64 \
libgomp1:amd64 \
libgomp1:arm64 \
libgomp1-arm64-cross \
libgomp1-armhf-cross \
libgomp1-powerpc-cross \
libgpg-error0:amd64 \
libgpm2:amd64 \
libgraphite2-3:amd64 \
libgssapi-krb5-2:amd64 \
libgssapi3-heimdal:amd64 \
libgvc6 \
libgvpr2 \
libharfbuzz0b:amd64 \
libhcrypto4-heimdal:amd64 \
libheimbase1-heimdal:amd64 \
libheimntlm0-heimdal:amd64 \
libhx509-5-heimdal:amd64 \
libice6:amd64 \
libidn11:amd64 \
libisl10:amd64 \
libisl10:arm64 \
libitm1:amd64 \
libitm1:arm64 \
libitm1-arm64-cross \
libjbig0:amd64 \
libjpeg-turbo8:amd64 \
libjpeg8:amd64 \
libjson-c2:amd64 \
libjson0:amd64 \
libjsoncpp0:amd64 \
libk5crypto3:amd64 \
libkeyutils1:amd64 \
libklibc \
libkmod2:amd64 \
libkrb5-26-heimdal:amd64 \
libkrb5-3:amd64 \
libkrb5support0:amd64 \
libldap-2.4-2:amd64 \
libllvm3.4:amd64 \
libllvm3.9v4:amd64 \
liblocale-gettext-perl \
liblockfile-bin \
liblockfile1:amd64 \
liblog-message-simple-perl \
libltdl-dev:amd64 \
libltdl7:amd64 \
liblzma5:amd64 \
libmagic1:amd64 \
libmodule-pluggable-perl \
libmount1:amd64 \
libmpc3:amd64 \
libmpc3:arm64 \
libmpdec2:amd64 \
libmpfr4:amd64 \
libmpfr4:arm64 \
libncurses5:amd64 \
libncursesw5:amd64 \
libnewt0.52:amd64 \
libnih-dbus1:amd64 \
libnih1:amd64 \
libnuma-dev:amd64 \
libnuma-dev:arm64 \
libnuma1:amd64 \
libnuma1:arm64 \
libobjc-4.8-dev:amd64 \
libobjc4:amd64 \
libp11-kit0:amd64 \
libpam-cap:amd64 \
libpam-modules:amd64 \
libpam-modules-bin \
libpam-runtime \
libpam0g:amd64 \
libpango-1.0-0:amd64 \
libpangocairo-1.0-0:amd64 \
libpangoft2-1.0-0:amd64 \
libpathplan4 \
libpcap0.8:amd64 \
libpcap0.8:arm64 \
libpcap0.8:armhf \
libpcap0.8:powerpc \
libpcap0.8-dev \
libpcre3:amd64 \
libpipeline1:amd64 \
libpixman-1-0:amd64 \
libplymouth2:amd64 \
libpng12-0:amd64 \
libpod-latex-perl \
libpopt0:amd64 \
libprocps3:amd64 \
libpython-stdlib:amd64 \
libpython2.7:amd64 \
libpython2.7-minimal:amd64 \
libpython2.7-stdlib:amd64 \
libpython3-stdlib:amd64 \
libpython3.4-minimal:amd64 \
libpython3.4-stdlib:amd64 \
libquadmath0:amd64 \
libreadline6:amd64 \
libroken18-heimdal:amd64 \
librtmp0:amd64 \
libsasl2-2:amd64 \
libsasl2-modules:amd64 \
libsasl2-modules-db:amd64 \
libselinux1:amd64 \
libsemanage-common \
libsemanage1:amd64 \
libsepol1:amd64 \
libsfasan0-armhf-cross \
libsfatomic1-armhf-cross \
libsfgcc-4.8-dev-armhf-cross \
libsfgcc1-armhf-cross \
libsfgomp1-armhf-cross \
libsfstdc++-4.8-dev-armhf-cross \
libsfstdc++6-armhf-cross \
libsigsegv2:amd64 \
libslang2:amd64 \
libsm6:amd64 \
libsqlite3-0:amd64 \
libss2:amd64 \
libssl-dev:amd64 \
libssl-dev:arm64 \
libssl-dev:armhf \
libssl-dev:powerpc \
libssl-doc \
libssl1.0.0:amd64 \
libssl1.0.0:arm64 \
libssl1.0.0:armhf \
libssl1.0.0:powerpc \
libstdc++-4.8-dev:amd64 \
libstdc++-4.8-dev:arm64 \
libstdc++-4.8-dev-arm64-cross \
libstdc++-4.8-dev-armhf-cross \
libstdc++6:amd64 \
libstdc++6:arm64 \
libstdc++6-arm64-cross \
libstdc++6-armhf-cross \
libtasn1-6:amd64 \
libterm-ui-perl \
libtext-charwidth-perl \
libtext-iconv-perl \
libtext-soundex-perl \
libtext-wrapi18n-perl \
libthai-data \
libthai0:amd64 \
libtiff5:amd64 \
libtimedate-perl \
libtinfo-dev:amd64 \
libtinfo5:amd64 \
libtool \
libtsan0:amd64 \
libudev1:amd64 \
libusb-0.1-4:amd64 \
libustr-1.0-1:amd64 \
libuuid1:amd64 \
libvpx1:amd64 \
libwind0-heimdal:amd64 \
libx11-6:amd64 \
libx11-data \
libx32asan0 \
libx32atomic1 \
libx32gcc-4.8-dev \
libx32gcc1 \
libx32gomp1 \
libx32itm1 \
libx32quadmath0 \
libx32stdc++-4.8-dev \
libx32stdc++6 \
libxau6:amd64 \
libxaw7:amd64 \
libxcb-render0:amd64 \
libxcb-shm0:amd64 \
libxcb1:amd64 \
libxdmcp6:amd64 \
libxext6:amd64 \
libxml2:amd64 \
libxmu6:amd64 \
libxmuu1:amd64 \
libxpm4:amd64 \
libxrender1:amd64 \
libxt6:amd64 \
linux-libc-dev:amd64 \
linux-libc-dev:arm64 \
linux-libc-dev:armhf \
linux-libc-dev:powerpc \
linux-libc-dev-arm64-cross \
linux-libc-dev-armel-cross \
linux-libc-dev-armhf-cross \
linux-libc-dev-powerpc-cross \
llvm-3.4 \
llvm-3.4-dev \
llvm-3.4-runtime \
llvm-3.9 \
llvm-3.9-dev \
llvm-3.9-runtime \
locales \
lockfile-progs \
login \
logrotate \
lsb-base \
lsb-release \
m4 \
make \
makedev \
manpages \
manpages-dev \
mawk \
mime-support \
module-init-tools \
mount \
mountall \
mscgen \
multiarch-support \
ncurses-base \
ncurses-bin \
net-tools \
netbase \
netcat-openbsd \
ntpdate \
openssh-client \
openssl \
passwd \
patch \
perl \
perl-base \
perl-modules \
pkg-config \
plymouth \
procps \
python \
python-apt-common \
python-clang-3.9 \
python-minimal \
python2.7 \
python2.7-minimal \
python3 \
python3-apt \
python3-dbus \
python3-gi \
python3-minimal \
python3-pycurl \
python3-software-properties \
python3.4 \
python3.4-minimal \
readline-common \
resolvconf \
rsync \
rsyslog \
sed \
sensible-utils \
sgml-base \
shared-mime-info \
software-properties-common \
sudo \
sysv-rc \
sysvinit-utils \
tar \
tzdata \
ubuntu-keyring \
ubuntu-minimal \
ucf \
udev \
unattended-upgrades \
upstart \
ureadahead \
util-linux \
vim \
vim-common \
vim-runtime \
vim-tiny \
wget \
whiptail \
x11-common \
xauth \
xkb-data \
xml-core \
xz-utils \
zlib1g:amd64 \
zlib1g:arm64 \
zlib1g:armhf \
zlib1g:powerpc \
zlib1g-dev:amd64 \
zlib1g-dev:arm64 \
zlib1g-dev:armhf \
zlib1g-dev:powerpc

RUN cd $HOME && \
   CUNIT_VERSION=2.1-3 && \
   curl -sSOL https://github.com/Linaro/libcunit/releases/download/${CUNIT_VERSION}/CUnit-${CUNIT_VERSION}.tar.bz2 && \
   tar -jxf *.bz2 && \
   cd CUnit* && \
   libtoolize --force --copy && \
   aclocal && \
   autoheader && \
   automake --add-missing --include-deps --copy && \
   autoconf && \
   \
   ./configure --host=powerpc-linux-gnu --build=x86_64-linux-gnu --prefix=/root/cunit-install/powerpc-linux-gnu && \
   make -j $(nproc) && \
   make install && \
   \
  ./configure --host=arm-linux-gnueabihf --build=x86_64-linux-gnu --prefix=/root/cunit-install/armhf && \
   make -j $(nproc) && \
   make install && \
   \
   ./configure --host=arm-linux-gnueabihf --build=x86_64-linux-gnu --prefix=/root/cunit-install/armhf && \
   make -j $(nproc) && \
   make install && \
   \
   ./configure --host=aarch64-linux-gnu --build=x86_64-linux-gnu --prefix=/root/cunit-install/aarch64 && \
   make -j $(nproc) && \
   make install && \
   cd -

RUN mkdir -p $HOME/download && cd $HOME/download && \
	apt-get download libpcap0.8-dev:arm64 && \
	apt-get download libpcap0.8-dev:armhf


RUN update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.9 100 && \
    update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.9 100
