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

Processor Modes
---------------
- Only Ring 0 used
- TLBs (D and I) are set to
  - 0x00000000-0x1FFFFFFF: Illegal
  - 0x20000000-0x5FFFFFFF: RWX, Cache Write-Through
  - 0x60000000-0xFFFFFFFF: RWX, Bypass Cache

References
----------
- [Chinese seller with boot modes](http://detail.1688.com/offer/40258194242.html?tracelog=gsda_offer)
- [Translated boot modes](https://drive.google.com/file/d/0ByLNRzaQc0jPV0xaektpdFFoMGs/edit)
- ESP8266_Module Application Design Guide Chinese.pdf