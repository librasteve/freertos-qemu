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


## SOC

- some errors when the Print (to LCD) task is enabled

```Timer with period zero, disabling
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
ssd0303: error: Unknown command: 0x80
ssd0303: error: Unexpected byte 0xe3
FreeRTOS command server.
Type help to view a list of registered commands.

>ts
Command not recognised.  Enter 'help' to view a list of available commands.


[Press ENTER to execute the previous command again]
>task-stats
Task        State   Priority  Stack    #
************************************************
CLI      	X	3	438	1
IDLE     	R	0	44	4
Status   	B	2	38	2
Print    	B	4	36	3

[Press ENTER to execute the previous command again]
```

- will comment => remove all the LCD and Status (hard button) code
- add ProcA and ProcB and Channel1 -- need to see the state of the channel queues
- iamerejh add in queue message monitor CLI Task