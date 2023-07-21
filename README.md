# openwrt-redmi-ax3000

`Openwrt` for `TP-Link AX55`

**!!! NOTE: This is the main development branch which using mainline `Linux LTS 5.4` !!!**

| Device        | Boot | Switch | CPU Ethernet | NSS NAT | 2.4G WiFi   | 5G WiFi |
| :-:           | :-:  | :-:    | :-:          | :-:     | :-:         | :-:     |
| TP-Link AX55  | ✔️¹  | ✔️     | ✔️          | ❌      | ❌         | ❌    |

> NOTE¹: Boot from RAM only. Because nand driver give error

## How to build

OS: `Ubuntu 20.04 (focal)`

```bash
# Install dependencies
sudo apt update
sudo apt install build-essential clang flex g++ gawk gcc-multilib gettext \
  git libncurses5-dev libssl-dev python3-distutils rsync unzip zlib1g-dev

# Clone this repo
git clone https://github.com/N1kroks/openwrt-tplink-ax55
cd openwrt-tplink-ax55

# Update and install feeds
./scripts/feeds update -a
./scripts/feeds install -a

# Configure
make menuconfig

# Download
make -j16 download

# Build
make -j$(nproc)
```

## How to install

### Flash Openwrt

#### a. Use `U-boot` to flash

Build openwrt and put it into TFTP root.

Then run the following command inside `U-boot`:

```shell
# This router ip
setenv ipaddr 192.168.1.2
# TFTP server ip
setenv serverip 192.168.1.1

# Download the firmware to the RAM
tftpboot openwrt-ipq50xx-arm-tplink_ax55-initramfs-fit-uImage.itb

# Boot openwrt from ram
setenv bootargs
bootm
```

## Related links

[`openwrt/openwrt`](https://github.com/openwrt/openwrt) - Openwrt official repository

[`qsdk`](https://git.codelinaro.org/clo/qsdk) - QSDK official repository

[`quic/qca-sdk-nss-fw`](https://github.com/quic/qca-sdk-nss-fw) - NSS firmware

[`quic/upstream-wifi-fw`](https://github.com/quic/upstream-wifi-fw) - WiFi firmware

[`qca/qca-swiss-army-knife`](https://github.com/qca/qca-swiss-army-knife) - BDF tools

[`Telecominfraproject/wlan-ap`](https://github.com/Telecominfraproject/wlan-ap) - another Openwrt which support `ipq50xx`
