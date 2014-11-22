This assumes you have the [[Toolchain]] set up. Note that compiling to support OTA upgrades is beyond the scope of this tutorial.

## Blinky, A Community Example
**Note:** This is using a fork of the examples that has fixes to build more easily. Use `https://github.com/esp8266/source-code-examples.git` once it has has been fixed.

```
cd /opt/Espressif
git clone https://github.com/tommie/source-code-examples.git
cd source-code-examples/blinky
make
```
You have two built files; `firmware/0x00000.bin` and `firmware/0x40000.bin`. That's it! Move on to [[Uploading]] to a device, unless you want to try building the examples provided by Espressif.

## Compiling Espressif's Examples
Choose one of the examples to build. Either the AT demo, pre-programmed in a lot of devices, or the IoT demo included with the ESP IoT SDK.

### The AT Demo
```
cd /opt/Espressif/ESP8266_SDK
wget -O at_v0.19_14_10_30.zip http://bbs.espressif.com/download/file.php?id=13
unzip at_v0.19_14_10_30.zip
cd at_v0.19_on_SDKv0.9.2
make
```
This should be enough before [Preparing the Firmware Image](#preparing-the-firmware-image).

### The IoT Demo
```
cd /opt/Espressif/ESP8266_SDK/IoT_Demo
make
```
This should be enough before [Preparing the Firmware Image](#preparing-the-firmware-image).

## Preparing the Firmware Image
The following is encoded in `app/gen_misc.sh`, but we use the crosstool-NG binutils, and the paths are off-by-one, so we show it in full here. We also use [esptool](https://github.com/tommie/esptool-ck) rather than `genflashbinv6.exe` to not require Windows. If you are following the Blinky example, what is described in this section has already been done by `make` for you, so reading this is optional.

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