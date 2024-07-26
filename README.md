# freertos-qemu
Using qemu to run freertos on cortex-m3

## Install
### ubuntu
    sudo apt-get install gcc-arm-none-eabi \
    binutils-arm-none-eabi gdb-multiarch openocd

    sudo apt install qemu-system-arm
### mac
    brew install --cask gcc-arm-embedded
    brew install aarch64-elf-gdb
    brew install openocd
    brew install arm-none-eabi-binutils
    brew install qemu
    
## Build
    git clone https://github.com/mghicho/freertos-qemu
    cd freertos-qemu
    git submodule init
    git submodule update --recursive
    cd CORTEX_LM3S811_GCC
    make

## Build from FreeRTOS
    git clone https://github.com/librasteve/FreeRTOS.git
    cd FreeRTOS
    git submodule init
    git submodule update --recursive
    cd CORTEX_LM3S811_GCC
    make


## Run
    qemu-system-arm -M lm3s811evb -nographic -kernel gcc/RTOSDemo.bin

use Ctrl-A+X to exit.
