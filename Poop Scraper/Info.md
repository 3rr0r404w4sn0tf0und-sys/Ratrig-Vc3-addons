### **💩 Poop Scraper:**
1. Take measurements from the printer nozzle to the 3030 frame         -  86mm   - 3.39 in -
2. Measure from the aluminum plate to the 3030 frame                   - 72.64mm - 2.86 in -
---
**💰 BOM:**

- [NEMA 17 Stepper](https://www.amazon.com/STEPPERONLINE-Stepper-Bipolar-42x42x38mm-Connector/dp/B0B38GX54H)
- [Breadboard](https://www.amazon.com/Solderless-Breadboard-Boards-Flexible-Jumper/dp/B0GVD11LSS)
- [TMC2209](https://www.amazon.com/BIGTREETECH-TMC2209-Stepper-TMC2208-TMC2130/dp/B07ZPV4HFP)
- [M3 screw assorted kit](https://www.amazon.com/Fgruh-750PCS-Assortment-Washers-Assorted/dp/B0FGV5FCBN)
- [A3144](https://www.amazon.com/ALLECIN-Effect-AH3144E-Magnetic-Detector/dp/B0CZ6QXMZ2?)
- [Magnet](https://www.amazon.com/Magnets-Powerful-Permanent-Multi-Use-Printing/dp/B0H55FXL9W?)
- [Capacitors](https://www.amazon.com/ALLECIN-Electrolytic-Capacitor-0-24x0-47in-Capacitors/dp/B0CMQB1T9L?)
- [Resistor](https://www.amazon.com/BOJACK-Values-Resistor-Resistors-Assortment/dp/B08FD1XVL6?)
- [Wiper(Optional)](https://qidi3d.com/products/plus4-wiper-silicone-case?from_collection=plus-4-accessories)
- Material cost: $74.31 USD($2 less with amazon prime membership)

**THE ABOVE IS ASSUMING YOU HAVE A SUITABLE PSU WITH THE RIGHT RING TERMINAL CRIMPS, HIGH-TEMP FILAMENT E.G. ASA/ABS, THE RPI, SPARE M6 SCREWS, M6 T-NUTS, AND CONNECTORS**

---
**🖨️ Printing instructions:**
- Perimeters: 3 Walls
- Material: ASA, ABS, or PA6 **AVOID ALL LOW TEMPERATURE FILAMENTS, THEY WILL MELT**
- Infill type: GYROID(Or 3d honeycomb)
- Infill amount: 40-50%
- Top and bottom solid infill: 4 Layers
- Supports: Yes(Unless your printer has really and I mean REALLY good cooling)

My Printables link:
[Printables](https://www.printables.com/model/1930826-ratrig-vc3-silicone-wiper-and-poop-scraper)

**Wiring:**

My CIRKIT link:

[Wiring for scraper v1](https://app.cirkitdesigner.com/project/67648cf2-0054-428f-89f6-700b67266870)

Stepper motor: (Assuming you have to wire it manually; if it has a JST-GH or similar connector, just plug that in!)
1. A- to A1, A+ to A2
2. B- to B1, B+ to B2

TMC2209 and RPi

- STEP to GPIO 20 (pin 38)
- EN to GPIO 16 (pin 36)
- DIR to GPIO 21 (pin 40)
- DIAG isn't used in this build. If you want stall detection later, wire it to any spare GPIO.
- VM/VS to the 12V rail (red).
- The GND next to VM goes to the 12V rail's negative (blue). The two GND pins are different, so be careful.
  
<img width="865" height="297" alt="image" src="https://github.com/user-attachments/assets/bd69176b-89ed-4b84-a1dd-9200dd4f855a" />

- Connect MS1 to the same 3.3v rail as VIO/VDD connection

<img width="117" height="111" alt="image" src="https://github.com/user-attachments/assets/da7dd7f5-8b74-4008-9b12-aa3f1c791b64" />

(Above pictured: Correct GND; Below pictured: Wrong GND)

<img width="117" height="111" alt="image" src="https://github.com/user-attachments/assets/ee314361-6b05-45ba-9616-c33e71b0a908" />


- The OTHER GND goes to the logic ground rail, which is connected to the Pi's GND (pin 14).
- VIO/VDD goes to the logic 3.3V rail, which is connected to the Pi's 3V3 (pin 1), not the 5V pin. On diagrams, 3.3V may be labeled 3V3.

**WARNING**
AVOID GPIO 0, 1, 2, 3, 7, 8, 9, 10, 11

UART (single-wire)

- GPIO 15 (RXD, pin 10) goes directly to the driver's RX/PDN pin.
- GPIO 14 (TXD, pin 8) goes through a 1kΩ resistor to that same RX/PDN pin. The 1k resistor protects the pins from burnout.
- The driver's TX pin stays unconnected.

**THESE ARE NOT INTERCHANGEABLE UNLESS YOU TWEAK A SETTING IN THE PI TO ENABLE OTHER PINS TO DO UART**

Hall sensor (A3144)

- VCC to the Pi's 5V (pin 2). The sensor needs 4.5V or more.
- GND to the logic ground rail.
- OUT to GPIO 23 (pin 16).
- Put a 10kΩ pull-up resistor from OUT to 3.3V. NEVER pull it up to 5V, because that puts 5V into a 3.3V GPIO pin. (Alternatively, skip the resistor and enable the Pi's internal pull-up on GPIO 23 in code.)

**⚠️ REMEMBER TO ENABLE UART ON THE PI** (unless you want the motor running on hopes and dreams!)

1. Run `sudo raspi-config`
2. Go to **Interface Options → Serial Port**
3. "Would you like a login shell accessible over serial?" → **No**
4. "Would you like the serial port hardware enabled?" → **Yes**
5. Reboot (`sudo reboot`), because the Pi won't take the hint until you do

If you skip this, the Pi will happily sit there talking to nobody while the TMC2209 stares back in silence.

**CFG**
1. Download the CFG from here: [CFG](https://github.com/3rr0r404w4sn0tf0und-sys/Ratrig-Vc3-addons/blob/main/Poop%20Scraper/Code/Stepper.cfg)
2. Upload it to Printer Settings/Machine Settings
3. In printer.cfg, add the line: [include scraper.cfg]
 **IMPORTANT: ADD THIS LINE ABOVE THE DO NOT EDIT LINE**
4. Test it, if it collides with bed, increase 30 to 40 and try until it is good!
5. Video Tutorial soon!

---

<img width="1723" height="1580" alt="image" src="https://github.com/user-attachments/assets/6983b028-f538-4012-b8e8-8b7c49fb7d11" />
<img width="1723" height="1580" alt="image" src="https://github.com/user-attachments/assets/1a43c235-7e38-4709-8b01-1ee4f941ce57" />
<img width="1723" height="1580" alt="image" src="https://github.com/user-attachments/assets/a65cc812-a1f7-4ac0-8150-2293e23128d9" />
