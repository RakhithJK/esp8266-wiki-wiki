## Bootloader
Baudrate: 76800

## flashing segments
* in 0x00000 are the segments .text, .data and .rodata from the elf file
* in 0x40000 is the segment .irom0.text
* the one at 0x00000 is a multipart-file wit headers, checksums, etc., whereas the one at 0x40000 is a raw file

## Hi res image of the top layer
![](http://s.zeptobars.ru/ESP8266.jpg)
[Tnx to](http://zeptobars.ru/en/read/Espressif-ESP8266-wifi-serial-rs232-ESP8089-IoT)

[Full size](http://s.zeptobars.ru/ESP8266-HD.jpg)

Some unconfirmed info on what is what http://imgur.com/Crzy9aM