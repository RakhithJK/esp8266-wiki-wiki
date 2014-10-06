#Building the AT example
comment the line #include user_config.h from /opt/Espressif/ESP8266_SDK/include/osapi.h
```
cd ~
mkdir esp_sources
cd esp_sources
cp -R /opt/Espressif/ESP8266_SDK/examples/at at
cd at
wget -O Makefile https://raw.githubusercontent.com/esp8266/source-code-examples/master/example.Makefile
make
```
If the compiler gives a error remove ```#include<stdlib.h>``` from ```user/at_ipCmd.c```

Now see [[Uploading]]