# SM2235EGH 5-Channel Constant-Current LED driver. Was integrated in a 'LightingInside' bulb purchased from Amazon, but is most likely present in other bulbs.

This is NOT a bulb you can easily replace with an ESP8266. A custom circuit board or hand wiring will need to be done, as well as modification of the LED disc itself.

# IMPORTANT
--> make sure to copy both `SM2235.yaml` and `SM2235.h` <--

![image](https://esphome.io/_images/made-for-esphome-black-on-white.svg)
# SM2235EGH based tuya lamps support for ESPHome
Project based off of the excellent preliminary work done by [dbuezas](https://github.com/dbuezas/esphome-bp5758).
![image](./lamp-example.jpeg)

# dynamic range mode

The SM2235EGH chip only allows 1023 brightness levels per channel, what makes it as bad as any other lamp at having good colors at dim levels and going very dim at all.
To improve upon that, this custom component dynamically changes the maximum current settings. As an example, my particular lamp used 26mA as a maximum, making the minimum possible level equal to 26mA/1024=0.025mA, which is also its resolution. Using dynamic range, when the lamp is asked to go dim, the esp will tell the SM2235EGH chip to set the maximum current to 1mA instead, pushing the minimum  to 1mA/1024=0.001mA, so 26 times less power and 26 times the color resolution at dim levels.
This is not how this chip was designed to be used, so to avoid flickering it was necessary to change the max level continuously and in small increments instead of just using one threshold. As is, it is super smooth.


You can test how static (intended) vs dynamic range (my hack) perform by using the lamp effects in HA's UI. The difference is massive.

# Links:

* Original BP5758 Discord thread: https://discord.com/channels/429907082951524364/429907082955718657/944508806770065428
* Horrible Chinese>English translation of SM2235EGH chip datasheet: https://github.com/fuxxociety/esphome-bp5758/blob/main/SM2235EGH%20datasheet.pdf
