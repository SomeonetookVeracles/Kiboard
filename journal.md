---
Title: "Kiboard!"
Author: "Veracles"
Description: "A 60% keyboard I'm designing for my new desk, with additional features such as a screen and a maximalist aesthetic"
Created On: "8/31/2025"
---

# August 31st - Setup

I started the project offf by setting up the initial schematic, opening Kicad and installing all the necessary libraries. For the MCU I used an ATMega32U4, which had it's... downsides, along with needing a dedicated clock on the board, as well as being incredibly expensive for the capabilities (5$ + 2.5kb ram hurts the soul), there are only 25 GPIO pins, and 5 power pins that need each of their own decoupling capacitors, this was exhausting to deal with, so I decided to go ahead and try out a new competitor I previously overlooked: The ESP-32 Wroom:

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

This is the new design, the schematic is also better, you can see that the designer actually labelled the pins with their alt functions, it's not a huge thing but I like the thought put into it. I also put the USB receptacle on it, I'm using a basic SMD connector for simplicity's sake, they're also slightly easier to wire up than the THT design.

<div align="center">
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/78e5e3b2-1766-4d09-93be-44f66375184f" style="width:80%; height:auto;"/>
</div>

Focusing on the USB receptacle real quick, the resistors connected to CC1 and 2 are 5.1k, enabling power reception and allowing reversible input for the plug itself. SBU1 and SBU2 are unecessary for the USB 2.0 speeds we'll be using for this, so we can just leave those disconnected for this. 


Now for the switches themselves.

I'm a lazy guy, so instead of manually measuring and positioning individual switches on the board, I'll be using an [online editor](https://www.keyboard-layout-editor.com/), and a [plugin](https://github.com/darakuneko/keyboard-layouter) for Kicad designed specifically for this purpose.

I started off by looking at some inspiration, and after immediately getting bored of that, I decided to do a 84 switch board, giving me a compact design while also giving me access to fn and specialist keys, I also will be extending the pcb 30mm on the left (not shown on the image), giving me space for the microcontroller and screen without any interference from other parts. 

<div align="center">
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c3747761-c5c9-43fa-81c9-049c7b7ea7e3" style="width:80%; height:auto;"/>
</div>

I saved this layout as a JSON file, and got back to the schematic.

<div align="center">
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d883aed9-8b57-4acd-8133-2c26c70d2bbb" style="width:80%; height:auto;"/>
</div>

This is the main layout of each individual switch (I'll get around to adding LEDs later)

<div align="center">
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/15952da8-0599-44ef-9b9a-c4c76779a7de" style="width:80%; height:auto;"/>
</div>

I'll be making this hotswappable using [this module from JLPCB](https://www.lcsc.com/product-detail/C41430893.html), it looks like a knockoff of the standard ones used for KaliH pcbs and should work perfectly fine.

Now we're ready to go and make the initial PCB, before adding on additional doodads like rotary endoders and the screen.

But I'm hungry, and it's 9pm, so I'm gonna make dinner and probably work on roulette, so I'll do that tomorrow.

#### Total time spent: 4.5h
