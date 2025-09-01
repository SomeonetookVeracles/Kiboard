---
Title: "Kiboard!"
Author: "Veracles"
Description: "A 60% keyboard I'm designing for my new desk, with additional features such as a screen and a maximalist aesthetic"
Created On: "8/31/2025"
---

# August 31st - Setup

I started the project offf by setting up the initial schematic, opening Kicad and installing all the necessary libraries. For the MCU I used an ATMega32U4, which had it's... downsides, along with needing a dedicated clock on the board, as well as being incredibly expensive for the capabilities (5$ + 2.5kb ram hurts the soul), there are only 25 GPIO pins, and 5 power pins that need each of their own decoupling capacitors, this was exhausting to deal with, so I decided to go ahead and try out a new competitor I previously overlooked: The ESP-32 Wroom. 

![ESP32-WROOM-32E-N8R2](https://github.com/user-attachments/assets/d6b174e6-c8da-4ba3-853f-b7365afb59ae)

This is the ESP32-WROOM-32E-R2, it's got a much larger package than the ATMega32U4 (like 3 times the size), but after making a comparison chart:

<div align="center">
  
  
| Feature       | ESP32‑WROOM‑32E‑R2               | ATmega32U4                    |
|--------------|----------------------------------|-------------------------------|
| **CPU Speed** | Dual-core, 240 MHz               | 8-bit, 16 MHz                 |
| **RAM**       | 520 KB + 16 KB RTC               | 2.5 KB                        |
| **Bluetooth** | Yes (v4.2, Classic + BLE)        | No                            |
| **Size**      | 18 × 25.5 × 3.1 mm               | ~7×7 mm (QFN) or 10×10 mm     |
| **Cost**      | ~$2.50 – $3.30                   | ~$4.50 – $5.50                |

(look I centered it!)

(This is small but after looking at the documentation I decided to go for the module with 16mb of PSRAM so I can play around with animations and other cool stuff.)
</div>

As you can see, the only real benefit I would gain by using the atmega32u4 would be size, which is negligible anyways when making larger keyboards, and it'll actually reduce the cost of PCBA because I won't need an additional bluetooth module, and less capacitors.

Now that we've got the boring stuff out of the way, we can get to the actually interesting stuff, the schematics.

I started of by setting up the board, placing down the ESP-32 and decoupling capacitors Now I plan on adding a screen and a few other doodads to this, so I started by locating the SDA and SCL pin and (temporarily) marking them as unpopulated, so I don't accidentally use them when routing up the keyboard matrix. (I know I could just use a global net but I'm lazy and this gives me less of a headache.) I also crossed out the SENSOR_VP and SENSOR_VN pins because those are input only and I don't really need them (this might change later).

<div align="center">
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e0a40c1c-8720-46a3-a4e8-18171417c760" style="width:80%; height:auto;"/>
</div>
...





(Ok I'm gonna be so real here I got distracted and spent an hour and a half trying to find a component for the screen, and I ended up settling on the ST 7789, the one problem being I don't have a schematic for the exact model JLPCB supports assembling, so I instead am going to be adding it when I export it to EasyEDA later. )




...



Now, back to the original design, we have a small problem, that being that the ESP-32 WROOM 32E doesn't natively support USB connectivity, so I'll be swapping over to using the ESP-32-S3-WROOM-2, which has more GPIO, USB support, and up to 32mb of flash and 16mb of SRAM. Now, you might be asking why I didn't go for this in the original design, and well, I didn't know it existed, so we're doing this instead.

<div align="center">
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2696cbcd-4b25-419d-90f1-19f86344019e" style="width:80%; height:auto;"/>
</div>
