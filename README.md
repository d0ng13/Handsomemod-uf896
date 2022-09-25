*`[README.md](README.md)` last updated on: 2022-09-25.*

[![HandsomeMod logo](img/logo.thumb.png)](img/logo.png)

<p align="center"><img src="img/logo.png" /></p>

# HandsomeMod router operating system for "OpenStick" UF896.

This repository is a fork of the ["`uf896`"-branch](https://github.com/kirdesde/Handsomemod/tree/uf896) of "[kirdesde/Handsomemod](https://github.com/kirdesde/Handsomemod/)", which itself is based on "[HandsomeMod/HandsomeMod](https://github.com/HandsomeMod/HandsomeMod/)".

It is an operating system based on [OpenWrt](http://openwrt.org/), but with many changes and additions.

This repository here is especially targeted at supporting the UF896 LTE/WiFi routers which come in the form factor of an USB stick. A discussion about this devices with links to further projects can be found [here on the OpenWrt forum](https://forum.openwrt.org/t/131712).

<details><summary>Photographs (*click* to open):</summary>
[![00_-_topside.jpg](img/uf896/00_-_topside.jpg.thumb.jpg 00_-_topside.jpg)](img/uf896/00_-_topside.jpg) [![01_-_PCB_SoCside.jpg](img/uf896/01_-_PCB_SoCside.jpg.thumb.jpg 01_-_PCB_SoCside.jpg)](img/uf896/01_-_PCB_SoCside.jpg) [![02_-_PCB_SIMside.jpg](img/uf896/02_-_PCB_SIMside.jpg.thumb.jpg 02_-_PCB_SIMside.jpg)](img/uf896/02_-_PCB_SIMside.jpg) [![03_-_PCB_SoCside-with-antenna-and-heatsink-attached.jpg](img/uf896/03_-_PCB_SoCside-with-antenna-and-heatsink-attached.jpg.thumb.jpg 03_-_PCB_SoCside-with-antenna-and-heatsink-attached.jpg)](img/uf896/03_-_PCB_SoCside-with-antenna-and-heatsink-attached.jpg) [![04_-_PCB_SIMside-with-antenna-attached.jpg](img/uf896/04_-_PCB_SIMside-with-antenna-attached.jpg.thumb.jpg 04_-_PCB_SIMside-with-antenna-attached.jpg)](img/uf896/04_-_PCB_SIMside-with-antenna-attached.jpg) [![05_-_bottomside.jpg](img/uf896/05_-_bottomside.jpg.thumb.jpg 05_-_bottomside.jpg)](img/uf896/05_-_bottomside.jpg) [![06_-_cover_open_typesticker.jpg](img/uf896/06_-_cover_open_typesticker.jpg.thumb.jpg 06_-_cover_open_typesticker.jpg)](img/uf896/06_-_cover_open_typesticker.jpg)
</details>

Is is based on [OpenWrt 21.02](https://openwrt.org/releases/21.02/) and heavily modified. It uses a [Linux kernel](https://kernel.org/) version 5.10.33.

## Building

In general, the [building instructions from the OpenWrt project](https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem) apply, but different repositories are used.

To build the firmware for the UF896 from this repository, use the following steps:

1. Make sure you have the [OpenWrt build requirements](https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem) fulfilled.  
   *On [Artix Linux](http://artixlinux.org) and Artix based distributions, installing the [AUR package "`openwrt-devel`"](https://aur.archlinux.org/packages/openwrt-devel) does pull in all needed dependencies.*
2. Clone this repository: `git clone https://github.com/dreirund/Handsomemod-uf896.git`.
3. `cd` into the clone: `cd Handsomemod-uf896`.
4. Generate `feeds.conf` from the default: `cp feeds.conf.default feeds.conf`.
5. Make sure that in the `feeds.conf` the following feeds are enabled *(note that the "`packages`" feed comes from HandsomeMod and* not *from OpenWrt, and also note the extra "`handsomefeed`" feed)*:  
   ```
   src-git packages https://github.com/HandsomeMod/packages.git
   src-git luci https://git.openwrt.org/project/luci.git;openwrt-21.02
   src-git routing https://git.openwrt.org/feed/routing.git;openwrt-21.02
   src-git telephony https://git.openwrt.org/feed/telephony.git;openwrt-21.02
   src-git handsomefeed https://github.com/HandsomeMod/handsomefeed.git
   ```  
   *(Other feeds might be available as well.)*
6. Install packages from the feeds: `./scripts/feeds update -a && ./scripts/feeds install -a`.
7. Select the default configuration for the `UF896`:  
   1. `make menuconfig`,
   2. Select the following options:
      1. `Target System`: `Qualcomm Msm89xx Soc` (`CONFIG_TARGET_msm89xx=y`),
      2. `Subtarget`: `Msm8916 Soc based Targets` (`CONFIG_TARGET_msm89xx_msm8916=y`),
      3. `Target Profile`: `Openstick UF896` (`CONFIG_TARGET_msm89xx_msm8916_DEVICE_openstick_uf896=y`),
      4. Select `Save` and then `Exit` the configuration (*do not* do further configurations now).
   3. Generate default configuration for the selected target: `make defconfig`.
8. If you want, configure options to your liking now: `make menuconfig`.
9. Build the firmware image: `make`.

For more build options and troubleshooting, refer to the [OpenWrt build system usage](https://openwrt.org/docs/guide-developer/toolchain/use-buildsystem) and other [documentation at OpenWrt.org](https://openwrt.org/docs/).

## Installing

*tbd*

## State of this repository

This is work in progress and might not work as expected. The main work to make this work has been carried out by the upstream projects "[kirdesde/Handsomemod](https://github.com/kirdesde/Handsomemod/)" and "[HandsomeMod/HandsomeMod](https://github.com/HandsomeMod/HandsomeMod/)", many thanks to them.

## License

HandsomeMod itself (i.e. the code that is directly provided by the HandsomeMod repositories) is licensed under [GPL-2.0](LICENSES/GPL-2.0).

Building a HandsomeMod firmware might pull in other, external software, which might have it's own licensing.

## Original upstream README

*[Here to the original `README.md`](README.handsomemod-upstream.md) from the [upstream repository](https://github.com/kirdesde/Handsomemod/).*
