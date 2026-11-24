## **🧠 My Ideas**
- Ratrig VC3 poop scraper, using a linear actuator to push/pull the poop
- Orbiter 2.5 spinnything(customizable) to show it is moving
- My own knomi-like device; a knomi is like a screen you can attach to the 3d printer toolhead, and I want to make my own using an ESP32-S3
- My own Raspberry Pi display mount for the printer that uses an ESP32's built-in GPIO sensing to be able to wake and sleep the screen and printer.
---

### **💩 Poop Scraper:**
1. Take measurements from the printer nozzle to the 3030 frame -  86mm   - 3.39 in -
2. Measure from the aluminum plate to the 3030 frame                   - 72.64mm - 2.86 in -
3. Find a linear actuator to fit this gap, preferred: 2.75 in when retracted, extend by at least 1 in.
---
**💰 BOM:**
```
- Linear actuator x1(insert link here)
- ESP32 S3(insert link here)
- Wiring(insert link here)
- Material cost(insert value here)
```
---
**🖨️ Printing instructions:**
- Perimeters: 3 Walls
- Infill type: (insert type here)
- Infill amount: (Insert value here)
- Top and bottom solid infill: 4 Layers
- Supports: Yes(Unless your printer ahs really and I mean REALLY good cooling)

**Wiring:**
Stepper motor: (Assuming you have to manually wire; if it has a JST-GH or similar connector, just plug that in!)
A- to A1, A+ to A2
B- to B1, B+ to B2

TMC2209 and RPI:
Step to any spare GPIO pin
EN to any spare GPIO pin
DIR to any spare gpio pin
Diag to any spare gpio pin
VM/VS to 12V-24V output(any you have)
GND next to it(Not other GND, there are 2 of them, be careful) to the Negative output of the SAME PSU
<img width="117" height="111" alt="image" src="https://github.com/user-attachments/assets/da7dd7f5-8b74-4008-9b12-aa3f1c791b64" />

(Above pictured: Correct GND, Below pictured: Wrong GND)

<img width="117" height="111" alt="image" src="https://github.com/user-attachments/assets/ee314361-6b05-45ba-9616-c33e71b0a908" />
The OTHER GND conencts to any spare GND on the RPI
VIO/VDD goes to the **3.3V** on the pi, not the 5V slot, on diagrams the 3.3v may be labeled **3V3**

**WARNING**
AVOID GPIO 0, 1, 2, 3, 7, 8, 9, 10, 11

TX goes to GPIO 14 **REMEMBER TO USE A 1KOHM RESISTOR INCASE OF BURNOUT**
RX goes to GPIO 15
THESE ARE NOT INTERCAHNGABLE UNLESS YOU TWEAK A SETTIN IN THE PI TO ENABLE OTHER PINS TO DO UART

---

<img width="762" height="616" alt="image" src="https://github.com/user-attachments/assets/3bef4b22-563c-4515-a773-2dd188ef95a8" />
<img width="762" height="616" alt="image" src="https://github.com/user-attachments/assets/584f82a6-3916-4b38-824f-fc2eb2ada767" />
<img width="762" height="616" alt="image" src="https://github.com/user-attachments/assets/05829e92-cbe2-4925-a104-25055156b4c4" />




