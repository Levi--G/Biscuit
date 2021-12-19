# Construction/Configuration

A minimum Biscuit tracker (before soldering ESP01 and IMU):
![](/img/Minimum.jpg)

Biscuit uses lots of PCB jumper pads to allow you to configure the hardware any way you want it. This page will go over all the choices in the best order of soldering and per feature, so pay attention to what you need/want.

## SMD components

Always start with soldering the SMD components from the smallest with most legs to the more simple large components, you will thank me later:

### ADC

If you want to enable ADC support you just need to solder the components on the right pads as shown below (pay attention with the ADC so every pin has a pad under it, one side will not have the middle pin, and doesn't have a pad if rotated correctly)
- 1x MCP3021 (I2C ADC)
- 1x 100nF capacitor 1206
- 1x 9.1k resistor 1206
- 1x 5.1k resistor 1206

![](/img/ADC.jpg)