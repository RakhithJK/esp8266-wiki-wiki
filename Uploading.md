Uploading code to the module

To upload to the module, configure the following pins:

| Pin | Level | 
| --- | ----- | 
| CH_PD | High |
| GPIO0 | Low |
| GPIO2 | High |

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