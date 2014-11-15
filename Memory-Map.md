This page describes the physical memory layout of the ESP8266 family.

Reset Vector
------------
The reset vector is 40000000h or 50000000h, which maps to internal ROM.

Memory Layout
-------------
|  Address  |  Name  |    Size    | Type | R/W | Description |
| --------- | ------ | ---------- | ---- | --- | ----------- |
| 3FF00000h | dport0 | 16         | I/O  | RW? | Memory-mapped I/O. |
| 3FF40000h | drom0  | <40000h    | ROM  | R?  | *Unconfirmed.* Known from the XT2000 memory map. |
| 3FF80000h | dram1  | <40000h    | RAM  | RW  | *Unconfirmed.* Known from the XT2000 memory map. |
| 3FFE8000h | dram0  | 80k        | RAM  | RW  | User data RAM. Available to applications. |
| 40000000h | brom?  | 64k        | ROM  | RW? | Internal ROM. May be writable somehow, but details unknown. |
| 40100000h | iram1  | 32k        | RAM  | RW  | Instruction RAM. Shadowed version of 40200000h. |
| 40200000h | irom0  | <100000h   | ROM  | RW  | SPI Flash ROM? |
| 40211000h | irom0  | <100000h   | ROM  | RW  | User application, slot 1. |
| 40240000h | irom0  | <100000h   | ROM  | RW  | User application start.   |
| 40251000h | irom0  | <100000h   | ROM  | RW  | User application, slot 2. |
| 50000000h | srom   | <1000000h  | ROM  | R?  | *Unconfirmed.* Known from the XT2000 memory map. |
| 60000000h | sram   | <4000000h  | RAM  | RW  | *Unconfirmed.* Known from the XT2000 memory map. |
| 70000000h | iocch  | <E000000h  | I/O  | RW? | Cached I/O. *Unconfirmed.* Known from the XT2000 memory map. |
| 80000000h | rambp  | <10000000h | RAM  | RW  | Uncached RAM. *Unconfirmed.* Known from the XT2000 memory map. |
| 90000000h | iobp   | <E000000h  | I/O  | RW? | Uncached I/O. *Unconfirmed.* Known from the XT2000 memory map. |

SPI Flash ROM Layout (without OTA upgrades)
-------------------------------------------
This is for ESP IoT SDK version 0.8 and above.

| Address | Size |           Name            |      Description      |
| ------- | ---- | ------------------------- | --------------------- |
|  00000h | 248k | app.v6.flash.bin          | User application      |
|  3E000h | 8k   | master_device_key.bin     | OTA device key        |
|  40000h | 240k | irom0text.bin             | SDK libraries, slot 1 |
|  7C000h | 8k   | esp_init_data_default.bin | Default configuration |
|  7E000h | 8k   | blank.bin                 | Filled with FFh. May be WiFi configuration. |

SPI Flash ROM Layout (with OTA upgrades)
----------------------------------------
This is for ESP IoT SDK version 0.8 and above, supporting OTA upgrades.

| Address | Size |         Name          |       Description        |
| ------- | ---- | --------------------- | ------------------------ |
|  00000h | 4k   | boot.bin              | Bootloader               |
|  01000h | 64k  | flash1.bin            | User application, slot 1 |
|  11000h | 180k | irom0text1.bin        | SDK libraries, slot 1    |
|  3E000h | 8k   | master_device_key.bin | OTA device key           |
|  40000h | 4k   |                       | Unused                   |
|  41000h | 64k  | flash1.bin            | User application, slot 2 |
|  51000h | 180k | irom0text1.bin        | SDK libraries, slot 2    |
|  7E000h | 8k   | blank.bin             | Filled with FFh. May be WiFi configuration. |

Exception Vectors
-----------------
Unconfirmed. From the XT2000 memory map.

|  Address  |      Name       |
| --------- | --------------- |
| 40000000h | Reset           |
| 40000010h | DebugException  |
| 40000020h | NMIException    |
| 40000030h | KernelException |
| 40000050h | UserException   |
| 40000070h | DoubleException |

References
----------
- [Forum post Memory Layout, p274](http://www.esp8266.com/viewtopic.php?f=5&t=9&start=30#p274)
- [Forum post Firmware Dump, p263](http://www.esp8266.com/viewtopic.php?f=6&t=39&start=10#p263)
- [Forum post Memory Layout, p889](http://www.esp8266.com/viewtopic.php?f=5&t=9&start=50#p889)
- [Forum post Cloud update documentation, p2486](http://www.esp8266.com/viewtopic.php?f=5&t=454#p2486)
- lx106-rc-2010.1/xtensa-elf/lib/xt2000-rt/memmap.xmm
- [ESP SDK linker scripts](https://github.com/metalheart/esp8266/tree/master/ld)
