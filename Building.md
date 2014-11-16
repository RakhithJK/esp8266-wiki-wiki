Choose one of the examples to build. Either the community-created AT example, or Espressif's IoT demo.

Building the AT Example
-----------------------
Remove the line `#include user_config.h` from `/opt/Espressif/ESP8266_SDK/include/osapi.h`.
```
cd ~
mkdir esp_sources
cd esp_sources
cp -R /opt/Espressif/ESP8266_SDK/examples/at at
cd at
wget -O Makefile https://raw.githubusercontent.com/esp8266/source-code-examples/master/example.Makefile
make
```
If the compiler gives an error, remove `#include <stdlib.h>` from `user/at_ipCmd.c`.

Building the IoT Demo from Espressif
------------------------------------
This assumes you have the [[Toolchain]] set up. Note that compiling to support OTA upgrades is beyond the scope of this tutorial.

```
cd /opt/Espressif/ESP8266_SDK/IoT_Demo
make
```

The following is encoded in `app/gen_misc.sh`, but we use the crosstool-NG binutils, and the paths are off-by-one, so we show it in full here. We also use [esptool](https://github.com/tommie/esptool-ck) rather than `genflashbinv6.exe` to not require Windows.

```
cd .output/eagle/debug/image
esptool -eo eagle.app.v6.out -bo eagle.app.v6.flash.bin -bs .text -bs .data -bs .rodata -bc -ec
xtensa-lx106-elf-objcopy --only-section .irom0.text -O binary eagle.app.v6.out eagle.app.v6.irom0text.bin
cp eagle.app.v6.flash.bin ../../../../../bin/0x00000.bin
cp eagle.app.v6.irom0text.bin ../../../../../bin/0x40000.bin
```

Now you have two files in `/opt/Espressif/ESP8266_SDK/bin/`, one with the application code and data (called `0x00000.bin`) and one with SDK code (called `0x40000.bin`).

Move on to [[Uploading]] to a device.
