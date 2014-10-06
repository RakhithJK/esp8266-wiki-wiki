> Information tnx to mamalala

There are several registers that allow setting/clearing a pin that is as output, making a pin an input or output, and reading an input pin. 

First i added these PROVIDE's to the main linker script, ```/Espressif/esp_iot_sdk_v0.9.1/ld/eagle.app.v6.ld```, to make those registers available:

```
PROVIDE(PIN_OUT = 0x60000300);
PROVIDE(PIN_OUT_SET = 0x60000304);
PROVIDE(PIN_OUT_CLEAR = 0x60000308);

PROVIDE(PIN_DIR = 0x6000030C);
PROVIDE(PIN_DIR_OUTPUT = 0x60000310);
PROVIDE(PIN_DIR_INPUT = 0x60000314);

PROVIDE(PIN_IN = 0x60000318);

PROVIDE(PIN_0 = 0x60000328);
PROVIDE(PIN_2 = 0x60000330);
```

In your C code or an include file you can then define these as external variables to access them:

```
extern volatile uint32_t PIN_OUT;
extern volatile uint32_t PIN_OUT_SET;
extern volatile uint32_t PIN_OUT_CLEAR;

extern volatile uint32_t PIN_DIR;
extern volatile uint32_t PIN_DIR_OUTPUT;
extern volatile uint32_t PIN_DIR_INPUT;

extern volatile uint32_t PIN_IN;

extern volatile uint32_t PIN_0;
extern volatile uint32_t PIN_2;
```

PIN_OUT is a register that holds the output of all the pins at once. Bit 0 = GPIO0, bit 2 = GPIO2. Whatever is written there will affect all the pins at once. For example, writing 0x01 will set GPIO0 high and GPIO2 low. Writing 0x04 will set GPIO2 high and GPIO0 low. 0x05 will set both high, 0x00 will set both low. That means that if you use multiple pins as output, you have to prepare what you write to this register, so as not to accidentally change any other pins that you don't want to change.

PIN_OUT_SET is a register that only sets a pin to high. Any bit that is that is set will set that pin high, any non-set pins will have no effect at all. For example, lets assume that GPIO0 and GPIO2 are both low. Writing 0x01 to that register will set GPIO0 to high. Now writing 0x04 to it will set GPIO2 high, while GPIO remains unchanged, that is, still high. This is useful to set a specific pin quickly without having to mask other pins, the chip will do that on it's own.

PIN_OUT_CLEAR is like _SET, just that any "1" bit will set the according pin to low. So, continuing the above, writing 0x01 to this register will no set GPIO0 to low, while GPIO2 still remains high, then writing 0x04 will set GPIO2 to low.

PIN_DIR is organized like PIN_OUT, that is, it affects all pins at once. Any bit that is set will make that pin an output. Writing 0x05, for example, will make GPIO0 and GPIO2 outputs, writing 0x01 will make GPIO0 an output and GPIO2 an input, etc.

PIN_DIR_OUTPUT is like PIN_OUT_SET, only that this changes the direction of the pin to an output instead of it's output level. Subsequently, PIN_DIR_INPUT sets pins as an input. Again, only "1" bits written will cause a change.

PIN_IN holds the input states of the pins. Any "1" bit means that the relevant pin sees a logic high, any "0" bit indicates a logic 0. These bits change regardless wether the pin is configured as output or input. Setting a pin as output and then setting it high will also set the bit for that pin in this register to high, for example.

Now, above i also gave addresses for PIN_0 and PIN_2. As of yet i have no idea what these do. I guess those are for configuring specific pins somehow. Not all bits can be set in, for example, PIN_2. Depending on what the output state is, i can toggle the pin by toggling bit 0 there, but i am unsure if that does hard-drive the pin or if some pull-up/down stuff is fooling me there.

Anyways, the _OUT_SET and _OUT_CLEAR registers are quite useful, so are the _DIR_OUTPUT and _DIR_INPUT registers if one wants to quickly set/clear pins or change their direction, without going through the provided API, which always takes 4 parameters that are handed over to a function in ROM and then subsequently used there. Directly accessing them will reduce that overhead.

Oh, and of course the PIN_OUT and PIN_DIR registers can also be read back (but not the set/clear and input/output registers, they will always return 0 on read)