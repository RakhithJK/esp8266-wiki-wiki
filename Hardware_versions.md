## ESP-01, Versions 1 and 2
<img title="Version 1" src="https://github.com/esp8266/esp8266-wiki/blob/master/images/module_v1.jpg" height="200px">
<img title="Version 2" src="https://github.com/esp8266/esp8266-wiki/blob/master/images/module_v2.png" height="200px">

### Info
For enabling the chip in the second version, bind pin `CH_PD` to `VCC` (3.3v).

### Pins to chip names
| Pin |   Name   | Description |
| ---:| -------- | ----------- |
| 1   | GND      | Ground
| 2   | U0TXD    | UART0 Transmit
| 3   | GPIO2    | Has internal pull-up
| 4   | CHIP_EN  | Chip Enable, active high
| 5   | GPIO0    | Has internal pull-up
| 6   | EXT_RSTB | External reset signal, active low, has no pull-up? Spurious blue LED activity when attaching a DMM between GND and RST to check voltage.
| 7   | U0RXD    | UART0 Receive, has internal pull-up
| 8   | VDD      | +3.3V power input

### LEDs
| Color | Name | Description
| ----- | ---- | -----------
| Red   | PWR  | Tied to VCC, so always on when power is applied
| Blue  | TXD  | UART TX indicator, tied in hardware to U0TXD

## ESP-03
![](https://github.com/esp8266/esp8266-wiki/blob/master/images/esp-03.jpg)
### Info
Starting the module bind CH_PD to VCC (3.3v) and GPIO15 to GND

## ESP8266MOD
![](https://github.com/esp8266/esp8266-wiki/blob/master/images/esp-mod.jpg)

## References
- [Forum post Status LEDs, p2183](http://www.esp8266.com/viewtopic.php?f=13&t=473#p2183)
