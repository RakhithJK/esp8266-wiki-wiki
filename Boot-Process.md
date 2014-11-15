Overview
--------
- Reset vector is 40000000h (unconfirmed).
- Boots into Xtensa SROM (unconfirmed).
- Transfers control to Espressif code in IROM0 (unconfirmed).
- Starts executing ESP SDK-code shadowed SPI ROM (unconfirmed).

ESP Boot Modes
--------------
The Espressif code can boot in different modes, selected on power-up based on GPIO pin levels.

| MTDO | GPIO0 | GPIO2 | Mode  | Description
|:----:|:-----:|:-----:| ----- | -----------
|   L  |   L   |   H   | UART  | Download code from UART
|   L  |   H   |   H   | Flash | Boot from SPI Flash
|   H  |   x   |   x   | SDIO  | Boot from SD-card

References
----------
- [Chinese seller with boot modes](http://detail.1688.com/offer/40258194242.html?tracelog=gsda_offer)
- [Translated boot modes](https://drive.google.com/file/d/0ByLNRzaQc0jPV0xaektpdFFoMGs/edit)
- ESP8266_Module Application Design Guide Chinese.pdf