# MicroPython STM32 compile process in Ubuntu 18.02

How to compile micropython stm32 in ubuntu 18.02 

It is not recommended to compile the firmware yourself, just use the firmware provided by us. If you really need to compile, please bring your own basic Linux knowledge. The following are the operations under Linux

Install dependencies:
``` sh
sudo apt update
sudo apt install -y build-essential git libffi-dev pkg-config gcc-arm-none-eabi binutils-arm-none-eabi libnewlib-arm-none-eabi python3
```
remove only the gcc-arm-none-eabi
``` sh
sudo apt remove gcc-arm-none-eabi
```
download ARM architecture setup:

https://developer.arm.com/-/media/Files/downloads/gnu/11.2-2022.02/binrel/gcc-arm-11.2-2022.02-x86_64-arm-none-eabi.tar.xz?rev=99a2bce6f4464be08eca01eda13e4e96&hash=C371F8D384D7F8DC08BFE154352AA3AE

Extract the files to /usr/share/

Install dependencies Round#2:
``` sh
sudo apt install libncurses-dev
sudo ln -s /usr/lib/x86_64-linux-gnu/libncurses.so.6 /usr/lib/x86_64-linux-gnu/libncurses.so.5
sudo ln -s /usr/lib/x86_64-linux-gnu/libtinfo.so.6 /usr/lib/x86_64-linux-gnu/libtinfo.so.5
sudo ln -s /usr/share/gcc-arm-none-eabi-your-version/bin/* /usr/bin/
```
check the version:
``` sh
arm-none-eabi-gcc --version
arm-none-eabi-g++ --version
arm-none-eabi-gdb --version
arm-none-eabi-size --version
```
For the Micropython process compile 
clone micropython:
``` sh
git clone https://github.com/micropython/micropython.git
cd micropython
git submodule update --init
cd mpy-
make -j4
```
Select the board you would like to compile and compile it:

``` sh
cd ..
make BOARD=Your_Board_Folder -j
```
