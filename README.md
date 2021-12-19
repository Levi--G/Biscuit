# Biscuit

Biscuit is a small cookie that tracks you :3

Biscuit is a custom PCB for a [SlimeVR](https://github.com/SlimeVR/SlimeVR-Tracker-ESP) tracker focussed on features and broad compatibility while staying as small and cheap as you can get

![](/img/BiscuitFull.jpg)

Check how to build and configure one of these [here](Construction.md)

Check out the schematic/copmponent choice [here](Schematic.md)

## Features

- Supports a wide range of IMUs
- Allows selecting IMU source voltage (VBat, 3.3V, Lower V for example 1.8V)
- Supports converting voltage levels for I2C/INT pins
- Supports setting AD0 on internal IMU
- Supports Trackers with int and AD0 pins on different spots
- Supports extra pullup resistors for I2C and int pins in case external ones are not sufficient
- Has a debug header for easy serial access
- Optional external ADC MCP3021 support for measuring precise battery voltage
- Optional on-board Led with FET driver
- All resistors and caps are 1206 SMD format and chips are SOT23 allowing for full hand-soldering without need for solder paste and a reflow oven
- Holes for soldering external tracker ribbon cable with data lines apart for easy soldering

## Downsides

- Harder to upload new firmware
- Not all features are supported on one tracker (choices must be made)
- Battery management not included on pcb so an external tp4056 and switch is still needed

## Components needed

Biscuit is based on ESP-01 boards, you find these in batches of 5pcs for very cheap locally or on [ali](https://aliexpress.com/item/32693314450.html)
IMU can be chosen depending on the current support status of SlimeVR, check [THE DOCS](https://docs.slimevr.dev/components-guide.html) for that

Required per tracker:
- ESP-01 Board
- IMU
- 1x 10µF capacitor 1206
- 2x 1µF capacitor 1206
- 1x [ME6211C33M](https://aliexpress.com/item/32959896723.html) (3.3V LDO regulator)

There are several options that can be chosen:

### Level shifter

This extension allows for 1.8V IMUs (or other voltages smaller than 3.3V) like the ICM-20948 to be connected to the tracker.

Required per tracker:
- 1x ME6211 of the right voltage like [ME6211C18](https://aliexpress.com/item/1005002058216911.html) for 1.8v
- 2x 1µF capacitor 1206
- 2x [BSS138](https://aliexpress.com/item/32944629649.html) level shifters for I2C lines
- (Optional) 2x [BSS138](https://aliexpress.com/item/32944629649.html) level shifters for INT lines

Also foreseen are 8 spots to solder 1206 pullup resistors in case these are needed because either the IMU board doesn't supply them or they are not small enough. I2C pullup resistor values are a complicated topic of trial and error, if you are not sure you need these, do not solder any resistors.

Note: INT pins are not compatible with LED/Serial logging

### External ADC

The external ADC is the most expensive option on Biscuit, but it will give a good reading of the battery voltage and thus how full your batteries are. Recommended is that you add one or a few on a tracker with similar batteries and charge them together, this should give you a general status of all your trackers since they should last about the same time.

Required per tracker:
- 1x [MCP3021](https://aliexpress.com/item/32632899790.html) (I2C ADC)
- 1x 100nF capacitor 1206
- 1x 9.1k resistor 1206
- 1x 5.1k resistor 1206

### External LED

The external LED is not compatible with uploading wifi credentials over serial connection and the internal INT pin support. This LED can show status of the tracker.

Required per tracker:
- 1x basic single color 3mm LED (color of choice)
- 1x [BSS138](https://aliexpress.com/item/32944629649.html) FET
- 1x 3.3k resistor 1206

### Incompatibilities

Like mentioned before the ESP01 only has a few IO ports, that means not all features are compatible you need to choose like this:

TX pin:
- Serial logging of errors
- INT pin for external IMU (needed for BNO08x)

RX pin:
- Serial transmitting of wifi credentials and other commands
- External LED
- INT pin for internal IMU (needed for BNO08x)