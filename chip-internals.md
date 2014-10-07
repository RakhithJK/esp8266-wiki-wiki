## flashing segments
* in 0x00000 are the segments .text, .data and .rodata from the elf file
* in 0x40000 is the segment .irom0.text
* the one at 0x00000 is a multipart-file wit headers, checksums, etc., whereas the one at 0x40000 is a raw file
