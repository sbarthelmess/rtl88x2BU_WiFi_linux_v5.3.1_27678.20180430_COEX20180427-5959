# Driver for Realtek / Panda RTL88x2BU USB Wifi adaptors 
(Most hardware shows as ID 0bda:b812 from lsusb output)

These are the generic drivers for the AC1200 cards all over Amazon, great devices, but limited support and the binary drivers have WAY too much debugging enabled.  Use this to boost your signal strength significantly and squeeze about +5Mbit more out of your connection (YMMV, these are the results I got). 

NOTE: Updated driver for rtl88x2bu wifi adaptors based on rtl88x2BU_WiFi_linux_v5.3.1_27678.20180430_COEX20180427-5959 originally downloaded from [D-Link's download page for the DWA-182 Rev D](https://support.dlink.com/ProductInfo.aspx?m=DWA-182).

Build confirmed on:

```bash
Raspberri pi3b+ - Linux version 4.19.58-v7+ armv7l, running Raspbian dist upgraded to BUSTER
```
## Simple pre-built installation (for latest buster kernel as of 7/29/2019) ##

```bash
insmod 8812bu.ko
```

## Simple build instructions (on RPI) ##
```bash

cd rtl88x2BU_WiFi_linux_v5.3.1_27678.20180430_COEX20180427-5959
make
sudo make install

```

## DKMS installation

```bash
cd rtl88x2BU_WiFi_linux_v5.3.1_27678.20180430_COEX20180427-5959
VER=$(sed -n 's/\PACKAGE_VERSION="\(.*\)"/\1/p' dkms.conf)
sudo rsync -rvhP ./ /usr/src/rtl88x2bu-${VER}
sudo dkms add -m rtl88x2bu -v ${VER}
sudo dkms build -m rtl88x2bu -v ${VER}
sudo dkms install -m rtl88x2bu -v ${VER}
sudo modprobe 88x2bu
```

Thanks to @cilynx for finding and posting these originally!
