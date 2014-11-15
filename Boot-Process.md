Overview
--------
- Reset vector is 40000000h (unconfirmed).
- Boots into Xtensa SROM (unconfirmed).
- Transfers control to Espressif code in IROM0 (unconfirmed).
- Starts executing ESP SDK-code shadowed SPI ROM (unconfirmed).

ESP Boot Modes
--------------
The Espressif code can boot in different modes, selected on power-up based on GPIO pin levels.

| GPIO0 | GPIO2 | MTDO | Mode | Description
| ----- | ----- | ---- | ---- | -----------
|   L   |   H   |   L  | UART | Download code from UART
|   H   |   H   |   L  | SPI  | Boot from SPI Flash
|   x   |   x   |   H  | SDIO | Boot from SD-card

References
----------
- [Chinese seller with boot modes](http://detail.1688.com/offer/40258194242.html?tracelog=gsda_offer)
- [Translated boot modes](https://drive.google.com/file/d/0ByLNRzaQc0jPV0xaektpdFFoMGs/edit)
