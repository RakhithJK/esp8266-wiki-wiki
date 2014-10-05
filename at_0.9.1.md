**This still needs some work**
| Command  | Description | Set / Execute | Query | Test | Parameters |
| -------- | ----------- | ------------- | ----- | ---- | -------- |
| AT | General test | | | | |
| ATE | same as AT  | | | |
| AT+RST | Soft reset | | | |
| AT+GMR | Show software and SDK version
| AT+CWMODE | Wireless mode | AT+CWMODE=? | | | |  1=Station, 2=AP, 3=Hybrid(both)
| AT+CWJAP | Join a AP (only in mode 1 or 3 | AT+CWJAP="ssid","password" | AT+CWJAP? | | replace ssid with your network name and password with the network password (leave the quotes)
| AT+CWLAP | List the discoverd ssid's | | AT+CWLAP | | |
| AT+CWQAP | Leave the SSID | AT+CWQAP | | | |
| AT+CWSAP | Set the AP configuration (only in mode 2 and 3) | AT+CWSAP="ssid","password",channel,enc
| AT+CWLIF | Return ip address (only in mode 1 or 3) | AT+CWLIF 
| AT+CIFSR | 
| AT+CIPSTATUS | Return the connected tcp/udp clients/servers | AT+CIPSTATUS |||| <id>,<type>,<addr>,<port>,<tetype>= client or server mode
| AT+CIPSTART |  single connection (+CIPMUX=0) AT+CIPSTART= <type>,<addr>,<port> multiple connection (+CIPMUX=1) AT+CIPSTART= <id><type>,<addr>, <port> | | | |  id = 0-4, type = TCP/UDP, addr = IP address, port= port; eg. Connect to another TCP server, set multiple connection first: AT+CIPMUX=1; connect:  AT+CIPSTART=4,"TCP","X1.X2.X3.X4",9999
| AT+CIPCLOSE | Close the socket | AT+CIPCLOSE or AT+CIPCLOSE=id | | | replace id with the socket id
| AT+CIPSEND | Send data to socket | AT+CIPSEND=length
| AT+CIPMUX | 
| AT+CIPSERVER | 
| AT+CIPMODE | 
| AT+CIPSTO