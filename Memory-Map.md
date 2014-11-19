This page describes the physical memory layout of the ESP8266 family.

Reset Vector
------------
The reset vector is 40000080h, which maps to internal ROM.

Memory Layout
-------------
|  Address  |  Name  |    Size    | Type | R/W | Description |
| ---------:| ------ | ----------:|:----:| --- | ----------- |
| 00000000h |        |            | Exc  |     | Causes fault when reading.
| 20000000h |        |            | No   |     | Unmapped, repeated pattern of 00 80 00 00.
| 3FF00000h | dport0 |      1000h | I/O  | RW? | Memory-mapped I/O, repeated every 100h.
| 3FF10000h |        |            | No   |     | Unmapped, zeroes.
| 3FF20000h | ?      |            | ?    | RW? | Unidentified data.
| 3FF30000h |        |            | No   |     | Unmapped, zeroes.
| 3FFC0000h | ?      |     20000h | ?    | RW? | uint32 mapping to the address it is located at. What is this?
| 3FFE0000h |        |            | No   |     | Unmapped, zeroes.
| 3FFE8000h | dram0  |     14000h | RAM  | RW  | User data RAM. Available to applications.
| 3FFFC000h |        |      4000h | RAM  |     | ETS system data RAM.
| 40000000h | brom?  |     10000h | ROM  | RW? | Internal ROM. May be writable somehow, but details unknown.
| 40010000h |        |            | No   |     | Unmapped, zeroes.
| 40100000h | iram1  |     10000h | RAM  | RW  | Instruction RAM. Used by bootloader to load SPI Flash <40000h.
| 40110000h |        |            | ?    |     | Zeroes.
| 40140000h |        |            | ?    |     | Repeated pattern of 59 31 d8 ec.
| 40200000h |        |            | ?    |     | Zeroes. SPI Flash loads/is mapped here.
| 40300000h |        |            | ?    |     | Unmapped, repeated pattern of 00 80 00 00.
| 60000000h | ?      |      1000h | I/O  | RW? | Uncached I/O
| 60001000h | ?      |       800h | ?    | RW? | Uncached I/O
| 60001800h | ?      |       800h | ?    | RW? | Uncached. Mapped to 60001000h?
| 60002000h |        |            | Exc  |     | Causes fault when reading.
| 70000000h |        |  90000000h | No   |     | Unmapped, repeated pattern of 00 80 00 00.

SPI Flash ROM Layout (without OTA upgrades)
-------------------------------------------
This is for ESP IoT SDK version 0.8 and above.

| Address | Size |           Name            |      Description      |
| ------- | ---- | ------------------------- | --------------------- |
|  00000h | 248k | app.v6.flash.bin          | User application
|  3E000h | 8k   | master_device_key.bin     | OTA device key. *Unconfirmed:* Not used without OTA
|  40000h | 240k | app.v6.irom0text.bin      | SDK libraries
|  7C000h | 8k   | esp_init_data_default.bin | Default configuration
|  7E000h | 8k   | blank.bin                 | Filled with FFh. May be WiFi configuration

SPI Flash ROM Layout (with OTA upgrades)
----------------------------------------
This is for ESP IoT SDK version 0.8 and above, supporting OTA upgrades.

| Address | Size |         Name          |       Description        |
| ------- | ---- | --------------------- | ------------------------ |
|  00000h | 4k   | boot.bin              | Bootloader               |
|  01000h | 64k  | app.v6.flash1.bin     | User application, slot 1 |
|  11000h | 180k | app.v6.irom0text1.bin | SDK libraries, slot 1    |
|  3E000h | 8k   | master_device_key.bin | OTA device key           |
|  40000h | 4k   |                       | Unused                   |
|  41000h | 64k  | app.v6.flash1.bin     | User application, slot 2 |
|  51000h | 180k | app.v6.irom0text1.bin | SDK libraries, slot 2    |
|  7E000h | 8k   | blank.bin             | Filled with FFh. May be WiFi configuration. |

Exception Vectors
-----------------
|  Address  |      Name       |
| --------- | --------------- |
| 40000010h | DebugException  |
| 40000020h | NMIException    |
| 40000030h | KernelException |
| 40000050h | UserException   |
| 40000070h | DoubleException |
| 40000080h | Reset           |

Memmory-Mapped I/O Registers
----------------------------
Most of them live in 60000000h.

| Base Address | Size | Name  | Description
| ------------:| ----:| ----- | ---------------
|    60000000h |  80h | uart0 | The UART0 config registers, see `examples/IoT_Demo/include/drivers/uart_register.h`
|    60000300h |  74h | gpio  | *Unconfirmed:* The timer config registers, see `include/eagle_soc.h`
|    60000600h |  28h | timer | *Unconfirmed:* The timer config registers, see `include/eagle_soc.h`
|    60000700h |  A4h | rtc   | *Unconfirmed:* The RTC config registers, see `include/eagle_soc.h`
|    60000800h |  44h | iomux | The IO MUX config registers, see `include/eagle_soc.h`
|    60000F00h |  80h | uart1 | The UART1 config registers, see `examples/IoT_Demo/include/drivers/uart_register.h`

### iomux Pin Registers (60000804h&ndash;60000843h)

```
31    24       16        8        0
-------- -ffff--- -------- ud--UDEe
          `- Function      ||  |||`- Output Enable
                           ||  ||`- Output Enable during sleep
                           ||  |`- Pull-down during sleep
                           ||  `- Pull-up during sleep
                           |`- Pull-down
                           `- Pull-up
```

References
----------
- [Forum post Memory Layout, p274](http://www.esp8266.com/viewtopic.php?f=5&t=9&start=30#p274)
- [Forum post Firmware Dump, p263](http://www.esp8266.com/viewtopic.php?f=6&t=39&start=10#p263)
- [Forum post Memory Layout, p889](http://www.esp8266.com/viewtopic.php?f=5&t=9&start=50#p889)
- [Forum post Cloud update documentation, p2486](http://www.esp8266.com/viewtopic.php?f=5&t=454#p2486)
- lx106-rc-2010.1/xtensa-elf/lib/xt2000-rt/memmap.xmm
- [ESP SDK linker scripts](https://github.com/metalheart/esp8266/tree/master/ld)
