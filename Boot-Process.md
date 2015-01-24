Overview
--------
- Reset vector is 0x40000080.
- Boots into Espressif code in IROM0.
- Loads SPI ROM data.
- Starts executing ESP SDK-code shadowed SPI ROM (unconfirmed).

ESP Boot Modes
--------------
The Espressif code can boot in different modes, selected on power-up based on GPIO pin levels.

| MTDO | GPIO0 | GPIO2 | Mode  | Description
|:----:|:-----:|:-----:| ----- | -----------
|   L  |   L   |   H   | UART  | Download code from UART
|   L  |   H   |   H   | Flash | Boot from SPI Flash
|   H  |   x   |   x   | SDIO  | Boot from SD-card

In the bootup message 'boot mode:(x,y)' three low bits of x are {MTDO, GPIO0, GPIO2}.

Flow
----

### ResetHandler
- Set interrupt level 1
- Set processor modes (see separate section)
- Copy SROM data to SRAM
- Goto `_start`

### _start
- Set Ring 0
- Clear callback vector
- Set up stack at 3FFFFFFFh
- Call `main`

### main
- Initialize UART0
  - 115,200 bps, 8N1
  - `iomux.u0txd &= 0xE4F`
  - `iomux.gpio2 = (iomux.gpio2 & 0xECF) | 0x100`

Processor Modes
---------------
- Only Ring 0 used
- TLBs (D and I) are set to
  - 00000000h-1FFFFFFFh: Illegal
  - 20000000h-5FFFFFFFh: RWX, Cache Write-Through
  - 60000000h-FFFFFFFFh: RWX, Bypass Cache

References
----------
- [Chinese seller with boot modes](http://detail.1688.com/offer/40258194242.html?tracelog=gsda_offer)
- [Translated boot modes](https://drive.google.com/file/d/0ByLNRzaQc0jPV0xaektpdFFoMGs/edit)
- ESP8266_Module Application Design Guide Chinese.pdf
- [OTA bootloader, stage 1](https://github.com/esp8266/esp8266-wiki/blob/master/reversed/ota_bootloader_stage1.c)