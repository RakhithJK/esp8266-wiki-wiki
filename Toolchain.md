#Building the toolchain

##as root:
```
apt-get install git autoconf build-essential gperf bison flex texinfo libtool libncurses5-dev wget gawk libc6-dev-amd64
mkdir /opt/Espressif
chown $username /opt/Espressif 
```
(replace $username with the name of the local user)

##as local user:
```
/opt/Espressif
git clone -b lx106 git://github.com/jcmvbkbc/crosstool-NG.git 
cd crosstool-NG
./bootstrap && ./configure --prefix=`pwd` && make && make install
./ct-ng xtensa-lx106-elf
./ct-ng build
```

#Setting up the SDK
download esp8266_sdk_v0.9.1.zip:  http://rghost.net/download/58019758/eff3feb46a2047a0de0d56479d21fab434429fea/esp8266_sdk_v0.9.1.zip

extract esp8266_sdk_v0.9.1.zip to /opt/Espressif/ESP8266_SDK

#Adding libs to the SDK
wget -O /opt/Espressif/ESP8266_SDK/lib/libc.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libc.a
wget -O /opt/Espressif/ESP8266_SDK/lib/libhal.a https://github.com/esp8266/esp8266-wiki/raw/master/libs/libhal.a

#Installing ESP tool
Download the deb for esptool from the git repo or download the [source](https://github.com/esp8266/esp8266-wiki/raw/master/deb/src/esptool_0.0.2.orig.tar.gz) and build yourself.
```
dpkg -i esptool_0.0.2-1_i386.deb
```

Next step: [[Building]]
