To upload to the module, configure the following pins:

|  Pin   | Level | Description 
| ------ | ----- | -----------
| CH_PD  | High  | Enables the chip
| GPIO0  | Low   | Selects UART download [[boot mode|Boot-Process#esp-boot-modes]]
| GPIO2  | High  | Selects UART download [[boot mode|Boot-Process#esp-boot-modes]]
| GPIO15 | Low   | If availble. Selects UART download [[boot mode|Boot-Process#esp-boot-modes]]

Pinout is in [[Hardware versions|Hardware_versions]]

## Uploading
```
/opt/Espressif/esptool-py/esptool.py --port /dev/ttyUSB0 write_flash 0x00000 0x00000.bin
sleep 3
/opt/Espressif/esptool-py/esptool.py --port /dev/ttyUSB0 write_flash 0x40000 0x40000.bin
```

### Caveats
- Note to Windows users: For the port argument, use standard port names, e.g. `COM3`.
- Sometimes a reset is required between uploading the first and second file.
- There are some cases that the upload fails with "Failed to leave Flash mode". This is normal your upload went without issues.