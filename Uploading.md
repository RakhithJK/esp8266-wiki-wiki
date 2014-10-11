Uploading code to the module

To upload to the module configure the following pins

| Pin | Level | 
| --- | ----- | 
| CH_PD | High |
| GPIO0 | Low |
| GPIO2 | High |
Pinout is in [[Hardware versions|Hardware_versions]]
## Uploading
### [esptool.py](https://github.com/themadinventor/esptool/blob/master/esptool.py)
This will upload the first part of the software to the esp
```
esptool.py --port /dev/ttyUSB0 write_flash 0x00000 0x00000.bin
```

This will upload the second part (sometimes a reset is needed)
```
esptool.py --port /dev/ttyUSB0 write_flash 0x40000 0x40000.bin
```

There are some cases that the upload fails with "Failed to leave Flash mode" this is normal your upload went without issues.