Welcome to the esp8266 wiki!

## Current status
* A working GCC-based [[Toolchain]]
* Open-source tools for working with the firmware images and serial protocol
* A closed/NDA SDK (work is being done getting this into the open)


## What is this ESP8266
* It's a wireless [SoC](https://en.wikipedia.org/wiki/System_on_a_chip)
* It has GPIO, I2C, ADC, SPI, PWM and some more
* It's running at 80MHz
* 32KBytes of instruction RAM
* 96KBytes of data RAM
* 64KBytes boot ROM
* It has a Winbond [[W25Q40BVNIG]] SPI flash
* It's a RISC architecture
* The core is a 106micro Diamond Standard core (LX3) made by [Tensilica](http://ip.cadence.com/)
* The [[ESP8266 chip|Hardware_ESP8266 Versions]] is made by [Espressif](http://espressif.com/en/products/esp8266/)
* [[Modules|Hardware_versions]] bearing this chip are made by various manufacturers

## Features
* ￼802.11 b/g/n protocol
* Wi-Fi 2.4 GHz, support WPA/WPA2
* Super small module size (11.5mm x 11.5mm)
* Integrated 10-bit ADC
* Integrated TCP/IP protocol stack (ipv4 only at the moment)
* Integrated TR switch, balun, LNA, power amplifier and matching network Integrated PLL, regulators, and power management units
* +20dBm output power in 802.11b mode
* Supports antenna diversity
* Deep sleep power <10uA, Power down leakage current < 5uA
* Integrated low power 32-bit MCU
* SDIO 2.0, SPI, UART, [I2C](Drivers)
* STBC, 1x1 MIMO, 2x1 MIMO
* A-MPDU & A-MSDU aggregation & 0.4μs guard interval
* Wake up and transmit packets in < 2ms
* Standby power consumption of < 1.0mW (DTIM3)
* Operating temperature range -40C ~ 125C