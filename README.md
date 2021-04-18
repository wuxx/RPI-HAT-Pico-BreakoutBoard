PI-HAT-Pico-BreakoutBoard
-----------
[中文](./README_cn.md) [English](./README.md)

* [Introduction](#rpi-hat-pico-breakoutboard) 
* [Feature](#feature)
* [How to Use](#how-to-use)
	* [Serial](#serial)
	* [SWD](#swd)
* [Product Link](#product-link)
* [Reference](#reference)


# RPI-HAT-Pico-BreakoutBoard
Pico-BreakoutBoard is a user-friendly expansion board for Pico launched by MuseLab. The BreakoutBoard act as a raspberrypi hat, leads all GPIOs of Pico, and the pico is connected with SWD download interface and serial port provided by raspberrypi, which can be easily used for program & test of Pico.

<div align=center>
<img src="https://github.com/wuxx/RPI-HAT-Pico-BreakoutBoard/blob/master/doc/1.jpg" width = "500" alt="" align=center />
<img src="https://github.com/wuxx/rpi-hat-pico-breakoutboard/blob/master/doc/2.jpg" width = "500" alt="" align=center />
<img src="https://github.com/wuxx/rpi-hat-pico-breakoutboard/blob/master/doc/3.jpg" width = "500" alt="" align=center />
</div>


# Feature
- All GPIOs
- Serial
- SWD
- Reset

# How to Use
### Serial
raspberrypi | Pico
---|---
GND | GND
GPIO15/RXD | GP0/UART0_TX
GPIO14/TXD | GP1/UART0_RX

on raspberrypi, you can use the minicom or picocom to open the serial port, for example：
```
$sudo apt install minicom
$minicom -b 115200 -o -D /dev/serial0

$sudo apt install picocom
$picocom -b 115200 /dev/serial0

```
more details please reference getting-started-with-pico section 4.5


### SWD
Pico's onchiprom program implements a USB disk with drag-and-drop burning function, However, in some development scenarios, if you need to frequently modify the code and test, you need to repeatedly power down Pico, hold down the button and power up again, and wait for the USB enumeration to complete before you can drag and drop, which is a slightly tedious process. In fact, the Pico can be programmed & debugged through the SWD interface with the openocd, no need to re-power the Pico, just enter a command to complete, the detail is described as follows
1. install openocd
```
$ cd ~/pico
$ sudo apt install automake autoconf build-essential texinfo libtool libftdi-dev libusb-1.0-0-
dev
$ git clone https://github.com/raspberrypi/openocd.git --recursive --branch rp2040 --depth=1
$ cd openocd
$ ./bootstrap
$ ./configure --enable-ftdi --enable-sysfsgpio --enable-bcm2835gpio
$ make -j4
$ sudo make install
```

2. This repository has wrapped the command into scripts, after export the environments variables, you can call the script in any path, note that the format of the burn suffix is hex or bin, not the drag and drop uf2 file
```
$cd RPI-HAT-Pico-BreakoutBoard/tools
$source env.sh
$rfw xxx.hex/xxx.bin
```

more details please reference getting-started-with-pico section 5

# Product Link
[RPI-HAT-Pico-BreakoutBoard](https://www.aliexpress.com/item/1005002510961508.html?spm=2114.12010615.8148356.3.617667e7l3GCeX)

# Reference
### pico-sdk
https://github.com/raspberrypi/pico-sdk
### pico-examples
https://github.com/raspberrypi/pico-examples
### pico-lab
https://github.com/wuxx/pico-lab
