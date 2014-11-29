ESP8266EX chip pinout is something like this:

![ESP8266EX Pin Layout Diagram](https://github.com/esp8266/esp8266-wiki/blob/master/images/esp8266ex-layout.jpg)

Pin | Name | Type | GPIO | Function
:--:|------|:----:|------|----------
1 | VDDA | P | | Analog Power 3.0 ~3.6V
2 | LNA | I/O | | RF Antenna Interface,Chip Output Impedance=50 Ω No matching required but we recommend that the π- type matching network is retained.
3 | VDD3P3 | P | | Amplifier Power 3.0~3.6V
4 | VDD3P3 | P | | Amplifier Power 3.0~3.6V
5 | VDD_RTC | P | | NC(1.1V)
6 | TOUT | I  | | ADC Pin
7 | CHIP_EN | I | | Chip Enable. High: On, chip works properly; Low: Off, small current
8 |XPD_DCDC | I/O | | Deep-Sleep Wakeup;GPIO16
9 | MTMS | I/O | GPIO14 | HSPICLK
10 | MTDI | I/O | GPIO12 | HSPIQ
11 | VDDPST | P | | Digital/IO Power Supply (1.8V~3.3V)
12 | MTCK | I/O | GPIO13 | HSPID
13 | MTDO | I/O | GPIO15 | HSPICS
14 | GPIO2 | I/O | GPIO2 | UART Tx during flash progamming
15 | GPIO0 | I/O | GPIO0 | SPICS2
16 | GPIO4 | I/O | GPIO4 |
17 | VDDPST | P | | Digital/IO Power Supply (1.8V~3.3V)
18 | SDIO_DATA_2 | I/O | | Connect to SD_D2 (Series R 200Ω);SPIHD; HSPIHD
19 | SDIO_DATA_3 | I/O | | Connect to SD_D3 (Series R 200Ω); SPIWP; HSPIWP
20 | SDIO_CMD | I/O | | Connect to SD_CMD(Series R 200Ω); SPICS0
21 | SDIO_CLK | I/O | | Connect to SD_CLK (Series R 200Ω); SPICLK
22 | SDIO_DATA_0 | I/O | | Connect to SD_D0 (Series R 200Ω); SPIQ
23 | SDIO_DATA_1 | I/O | | Connect to SD_D1 (Series R 200Ω); SPID
24 | GPIO5 | I/O | GPIO5 |
25 | U0RXD | I/O | GPIO3 | UART Rx during flash progamming
26 | U0TXD | I/O | GPIO1 | UART Tx during flash progamming; SPICS1
27 | XTAL_OUT | I/O | | Connect to crystal output, can be used to provide BT clock input
28 | XTAL_IN | I/O | | Connect to crystal input
29 | VDDD | P | | Analog Power 3.0~3.6V
30 | VDDA | P | | Analog Power 3.0~3.6V
31 | RES12K | I | | Connect to series R 12kΩ to ground
32 |EXT_RSTB | I | | External reset signal (Low: Active)
Note: GPIO2, GPIO0, MTDO can be configurable as 3-bit SDIO mode 