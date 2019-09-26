FROM ubuntu:14.04

RUN apt-get update \
  && apt-get -y install sudo build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils wget build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint \
  && apt-get clean

RUN useradd -m openwrt \
  && echo 'openwrt ALL=NOPASSWD: ALL' > /etc/sudoers.d/openwrt

USER openwrt
WORKDIR /home/openwrt

RUN cd /home/openwrt \
  && git clone https://github.com/coolsnowwolf/lede \
  && cd lede \
  && git reset --hard 2915c44 \
  && git rm --cached package/lean/luci-app-ssr-plus -r \
  && git pull \
  && ./scripts/feeds update -a \
  && ./scripts/feeds install -a

COPY 14.04/default.config /home/openwrt/lede/.config

RUN cd /home/openwrt/lede \
  && make
