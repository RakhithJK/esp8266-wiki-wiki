This assumes you have the [[Toolchain]] set up. Note that compiling to support OTA upgrades is beyond the scope of this tutorial.

## Compiling
Choose one of the examples to build. Either the AT demo, pre-programmed in a lot of devices, or the IoT demo included with the ESP IoT SDK.

### The AT Demo
```
cd /opt/Espressif/ESP8266_SDK
wget -O at_v0.19_14_10_30.zip http://bbs.espressif.com/download/file.php?id=13
unzip at_v0.19_14_10_30.zip
cd at_v0.19_on_SDKv0.9.2
make
```
This should be enough before [[#Preparing the Firmware Image]].

### IoT Demo
```
cd /opt/Espressif/ESP8266_SDK/IoT_Demo
make
```

## Preparing the Firmware Image
The following is encoded in `app/gen_misc.sh`, but we use the crosstool-NG binutils, and the paths are off-by-one, so we show it in full here. We also use [esptool](https://github.com/tommie/esptool-ck) rather than `genflashbinv6.exe` to not require Windows.

```
cd .output/eagle/debug/image
esptool -eo eagle.app.v6.out -bo eagle.app.v6.flash.bin -bs .text -bs .data -bs .rodata -bc -ec
xtensa-lx106-elf-objcopy --only-section .irom0.text -O binary eagle.app.v6.out eagle.app.v6.irom0text.bin
cp eagle.app.v6.flash.bin ../../../../../bin/
cp eagle.app.v6.irom0text.bin ../../../../../bin/
```

Now you have two files in `/opt/Espressif/ESP8266_SDK/bin/`, one with the application code and data (called `...flash.bin`) and one with SDK code (called `...irom0text.bin`).

Move on to [[Uploading]] to a device.

## More Examples
More examples, like [Blinky](https://github.com/esp8266/source-code-examples/tree/master/blinky), can be found on GitHub, https://github.com/esp8266/source-code-examples.