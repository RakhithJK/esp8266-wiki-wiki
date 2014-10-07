# Compiler
**A big tnx goes out to [jcmvbkbc](https://github.com/jcmvbkbc) for making the compiler work**

Its build with crosstool, check [[Toolchain]] on how to install.

## stuff that still needs a place

### flashing segments
in 0x00000 are the segments .text, .data and .rodata from the elf file
in 0x40000 is the segment .irom0.text
the one at 0x00000 is a multipart-file wit headers, checksums, etc., whereas the one at 0x40000 is a raw file
