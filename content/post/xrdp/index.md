+++
title = "xrdp: building from sources"
date = "2024-05-14"
+++

> This page is under construction.

### Introduction

These are steps for building xrdp 0.10.0 and xorgxrdp 0.10.0, on Debian 12 (Ubuntu 24.04).

This page is refer to [Building on Debian 8](https://github.com/neutrinolabs/xrdp/wiki/Building-on-Debian-8) with backend `xorgxrdp`.

> Issue: *xrdp sink / source pulseaudio* modules: invalid ELF header, reported on Pixel 8.

### install.sh

```
apt update
apt install doas git
echo "permit nopass root as root" > /etc/doas.conf

cd ~
git clone https://github.com/neutrinolabs/xrdp
wget https://github.com/neutrinolabs/xrdp/releases/download/v0.10.0/xrdp-0.10.0.tar.gz
wget https://github.com/neutrinolabs/xorgxrdp/releases/download/v0.10.1/xorgxrdp-0.10.1.tar.gz
tar xzvf xrdp-0.10.0.tar.gz
cd ~/xrdp
./scripts/install_xrdp_build_dependencies_with_apt.sh max
apt install xorg
cd xrdp-0.10.0
./bootstrap
./configure --enable-fuse --enable-mp3lame --enable-pixman
make
make install
ln -s /usr/local/sbin/xrdp{,-sesman} /usr/sbin
cd ~
tar xzvf xorgxrdp-0.10.1.tar.gz
cd xorgxrdp-0.10.1
./bootstrap
./configure
make
make install
systemctl enable xrdp
service xrdp start
nano /etc/xrdp/sesman.ini /etc/xrdp/startwm.sh
```

