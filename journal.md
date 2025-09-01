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

</div>

As you can see, the only real benefit I would gain by using the atmega32u4 would be size, which is negligible anyways when making larger keyboards, and it'll actually reduce the cost of PCBA because I won't need an additional bluetooth module, and less capacitors.

