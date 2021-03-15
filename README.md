RPI-HAT-Pico-BreakoutBoard
-----------
[中文](./README.md) [English](./README_en.md)

* [介绍](#树莓派pico扩展板介绍) 
* [特性](#特性)
* [使用说明](#使用说明)
	* [串口](#串口)
	* [SWD下载](#swd下载)
* [产品链接](#产品链接)
* [参考](#参考)


# 树莓派Pico扩展板介绍 
树莓派Pico扩展板是MuseLab推出的方便用户使用Pico的扩展板，扩展板引出Pico所有GPIO，同时和树莓派提供的SWD下载接口、串口对接，利用树莓派提供的编译烧录调试环境，可以方便的对Pico进行烧录测试  
![top](https://github.com/wuxx/RPI-HAT-Pico-BreakoutBoard/blob/master/doc/top.jpg)
# 特性   
- 扩展板两侧引出所有GPIO  
- 串口，可通过拨码开关旁路  
- SWD下载调试接口  
- 复位按钮，用于复位Pico
- 扩展板兼容树莓派3/树莓派4  

# 使用说明
### 串口
树莓派的串口和Pico接线说明如下
树莓派 | Pico
---|---
GND | GND
GPIO15/RXD | GP0/UART0_TX
GPIO14/TXD | GP1/UART0_RX

树莓派上需要输入以下命令以启动硬件串口功能  
```
$sudo raspi-config
```
进入菜单 `Interfacing Options -> Serial`，先选择`No`，回车，然后选择`Yes`，保存退出即可。
启用串口后，可使用minicom或者picocom串口工具打开串口进行调试，举例如下：
```
$sudo apt install minicom
$minicom -b 115200 -o -D /dev/serial0

$sudo apt install picocom
$picocom -b 115200 /dev/serial0

```
更详细的说明，请参考getting-started-with-pico 4.5小节。


### SWD下载
Pico的onchiprom程序实现了一个U盘拖拽烧录的功能，可以通过拖拽uf2文件到虚拟U盘中实现烧录，然而在某些开发场景下，若需要频繁修改代码烧录测试，则需要反复将Pico下电，按住按键再重新上电，等待USB枚举完成，才能进行拖拽烧录，过程略微有些繁琐。 实际上可以通过Pico的SWD接口实现烧录调试，配合openocd开源调试软件，无需重新对Pico上下电，只需输入一条命令即可完成烧录，具体过程说明如下
1. 安装openocd
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
2. 本仓库已经封装好相应的脚本，导入环境变量之后即可在任意路径下调用烧录目标文件，注意烧录的格式后缀为`hex`或者`bin`，而非拖拽烧录的`uf2`文件。  
```
$cd RPI-HAT-Pico-BreakoutBoard/tools
$source env.sh
$rfw xxx.hex/xxx.bin
```

更详细的说明，请参考getting-started-with-pico 第5章节。

# 产品链接
[RPI-HAT-Pico-BreakoutBoard](https://item.taobao.com/item.htm?spm=a1z10.1-c-s.w4004-21349689053.18.305e20f8cSEvqA&id=614093598737)

# 参考
### pico-sdk
https://github.com/raspberrypi/pico-sdk
### pico-examples
https://github.com/raspberrypi/pico-examples
### pico-lab
https://github.com/wuxx/pico-lab
