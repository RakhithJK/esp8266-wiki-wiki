#Building the toolchain
## Install needed dependencies (as root)
### 32-Bit Debian (Linux)
```
apt-get install git autoconf build-essential gperf bison flex texinfo libtool libncurses5-dev wget gawk libc6-dev-amd64 python-serial libexpat-dev
mkdir /opt/Espressif
chown $username /opt/Espressif 
```

### 64-bit Debian (Linux)
```
apt-get install git autoconf build-essential gperf bison flex texinfo libtool libncurses5-dev wget gawk libc6-dev-i386 python-serial libexpat-dev
mkdir /opt/Espressif
chown $username /opt/Espressif 
```
(replace $username with the name of the local user)

### Windows
*By zoutepopcorn.*

- Use Python 2.7, **not** Python 3: https://www.python.org/downloads/
- Install pyserial-2.7: http://pyserial.sourceforge.net/pyserial.html

##Install the Xtensa crosstool-NG (as local user)
*A big thanks to [jcmvbkbc](https://github.com/jcmvbkbc) for making GCC and crosstool-NG work with the Xtensa call0 ABI!*

```
cd /opt/Espressif
git clone -b lx106 git://github.com/jcmvbkbc/crosstool-NG.git 
cd crosstool-NG
./bootstrap && ./configure --prefix=`pwd` && make && make install
./ct-ng xtensa-lx106-elf
./ct-ng build
PATH=$PWD/builds/xtensa-lx106-elf/bin:$PATH
```

If you install crosstool-NG outside of the build directory (by changing `--prefix` above), you need to copy `local-patches/` and `overlays/` to `<prefix>/lib/ct-ng.1.20.0/`

Note the default `xtensa-lx106-elf` configuration installs the compiler in `${CT_TOP_DIR}/builds/${CT_TARGET}`, not under `x-tools/`.

#Setting up the Espressif SDK
Download `esp_iot_sdk_v0.9.2_14_10_24.zip`: http://bbs.espressif.com/viewtopic.php?f=5&t=3

Extract the contends of `esp_iot_sdk_v0.9.2_14_10_24.zip` to `/opt/Espressif/ESP8266_SDK/`.

##Patching
- We use another toolchain.
- The IoT_Demo Makefile assumes it's one directory up (for libraries and linker script).

```
cd /opt/Espressif/ESP8266_SDK
sed -i -e 's/xt-ar/xtensa-lx106-elf-ar/' -e 's/xt-xcc/xtensa-lx106-elf-gcc/' -e 's/xt-objcopy/xtensa-lx106-elf-objcopy/' Makefile
mv examples/IoT_Demo .
```

#Installing Xtensa libraries and headers
```
wget -O /opt/Espressif/ESP8266_SDK/lib/libc.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libc.a
wget -O /opt/Espressif/ESP8266_SDK/lib/libhal.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libhal.a
wget -O /opt/Espressif/include.tgz https://github.com/esp8266/esp8266-wiki/raw/master/include.tgz
tar -xvzf include.tgz
```
These are binary libraries from the Xtensa SDK. You can also build them from source, but this has not yet been tested fully:
- [lx106-hal](https://github.com/tommie/lx106-hal) and
- [newlib-xtensa](https://github.com/jcmvbkbc/newlib-xtensa)

#Installing the ESP image tool
Download the deb for esptool from the Git repo or get the [source](https://github.com/esp8266/esp8266-wiki/raw/master/deb/src/esptool_0.0.2.orig.tar.gz) and build yourself. Also available as a [Git repository](https://github.com/tommie/esptool-ck) for online browsing.
```
dpkg -i esptool_0.0.2-1_i386.deb
```

#Installing the ESP upload tool
```
cd /opt/Espressif/
git clone https://github.com/themadinventor/esptool esptool-py
```

Next step: [[Building]]
