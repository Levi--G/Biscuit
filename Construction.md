# Construction/Configuration

A minimum Biscuit tracker (before soldering ESP01 and IMU):
![](/img/Minimum.jpg)

Biscuit uses lots of PCB jumper pads to allow you to configure the hardware any way you want it. This page will go over all the choices in the best order of soldering and per feature, so pay attention to what you need/want.

Jumper pads can best be soldered with just placing a big blob of solder that touches both ends (check the power section for an example), alternatively if you have this manufactured for you, you can solder a 0 Ohm resistor of 0603 footprint there. There are [plenty of tutorials](https://www.youtube.com/watch?v=yR_cIrmUS8A) of how to do this so i won't go into detail here.

## SMD components

Always start with soldering the SMD components from the smallest with most legs to the more simple large components, you will thank me later. All components just need to be soldered on the right pads as shown below if you want to enable the features, some are needed, some optional.

### (optional) ADC

Solder these if you want to enable (Option 2) ADC support. (pay attention with the ADC so every pin has a pad under it, one side will not have the middle pin, and doesn't have a pad if rotated correctly)
- 1x MCP3021 (I2C ADC)
- 1x 100nF capacitor 1206
- 1x 9.1k resistor 1206
- 1x 5.1k resistor 1206

![](/img/ADC.jpg)

### 3.3V Power

3.3V power is mandatory! Solder these components:
- 1x 10µF capacitor 1206
- 2x 1µF capacitor 1206
- 1x ME6211C33M

![](/img/3.3v.jpg)

### (optional) Low (1.8V) Power

If you have a IMU needing LV (1.8v for instance) and you plan on using level shifters, you will need these components to supply the lower voltage power:
- 1x ME6211 of the right voltage like ME6211C18 for 1.8v
- 2x 1µF capacitor 1206

![](/img/LV.jpg)

### Power Selection

This is where you select the right power for yout IMU, most imus on breakout boards have a onboard LDO converter to support 5V. CHECK THIS!
If:
- You are not sure and don't use level shifter, solder 3.3V
- Your IMU has a VCC converter solder 5V (Vbat)
- You have a 1.8V or low V board or use level shifters, solder LV

![](/img/Power.jpg)

### (optional) External LED

To use an external led (Option 3) you need to solder these components on the back of the print (wait with the actual LED):
- 1x [BSS138](https://aliexpress.com/item/32944629649.html) FET
- 1x 3.3k resistor 1206

![](/img/FET.jpg)

### (optional) Level Shifters

If you need level shifters (to a lower voltage) for the I2C/INT lines you need 2 BSS138 for the I2C lines, if you also need the INT pins (internal and/or external) you also need 1/pin.

All shifters are made the same way as seen in the image, if you don't want to use any shifters, skip to Bypass.

If you want to use I2C shifting, solder both BSS138 on the respective spots on the I2C lines as shown below. IF you **don't**, solder both bypass pads.

If you want to use INT pins AND logic shift them, solder the respective BSS138 on the correct pads, you do not have to solder both if you will not use them both, for instance you can enable just the internal INT pin and only solder that BSS138.

![](/img/Shifters.jpg)

### (optional) Pullups

If you know what you are doing and really need to add pullups to the I2C lines you can do that at the specified spots, it is however not recommended for any default design since both imu and esp already have pullups. It might however be needed when using logic level shifters. This is at own risk, a resistor too small might make communication impossible.

### Bypass

If you **do not** use one or more logic level shifters (default). You will need to solder the unused shifter's bypass jumpers. You can see the bypass jumper on the right of each of the shifter pads (check the image above). Make sure to not accidentally solder any other pads to the jumper, this may cause a short!

### INT & AD0 location and enabling

In order to Enable the INT and AD0 pins several jumpers are included:

![](/img/INT.jpg)

You can enable or disable as you please:
- Don't use INT pins? => don't solder any
- Don't want to enable internal AD0 => don't solder any.
- Want to enable internal INT? => Solder 1st or 2nd pin INT depending on where the INT pin is located on your board
- Want to enable internal AD0? => Solder 2nd or 3rd pin AD0...

And thats all SMD, now TH:

## Through Hole

todo