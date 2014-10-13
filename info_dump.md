

but other than that Tensilica doesn't make any peripherals itself instead it uses ones from OpenCores

iram/irom: there's no cache on this core, so the only buffer is the instruction decode buffer, which is like 4 or 8 bytes

ICACHE_FALSH_ATTR pushes the code to the serial flash