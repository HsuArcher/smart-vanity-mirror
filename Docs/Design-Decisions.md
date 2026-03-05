# Design Decisions
This document records major hardware and system level decisions for the smart vanity mirror.

---

## System Overview

Brief description of the system's main architecture

- ESP8266 Microcontroller
- Capactive touch sensors (MPR121)
- Addressable LED Strip
- USB-C Programmer port and Power input

---

## Power Decisions

### Power Input Selection
**Decision:** USB-C selected as the primary power source

**Reasoning:** 
The initial power source was a dedicated external 5V power supply. This however was too heavy and big to be a reasonable choice for a small desk sized vanity mirror. A USB-C port was already included in the schematic due to it being used to program the ESP8266 and was adapted to become a power input device.

**Notes:** 
- USB-C implemented to be in 5V mode 

---

### Input Protection
**Decision:** A polyfuse was added on the 5V input rail

**Reasoning:** 
For the longevity of the product and the safety of the user a polyfuse was added. The polyfuse provides protection against short circuit events and accidental overload.

**Notes:** 
- Polyfuse hold current is based on the worst case scenario for the current draw from the WS2812B RGB LED Strip and other electronics. 

---

### Voltage Regulator

**Decision:** a buck regulator is used to convert 5V to 3.3V

**Reasoning:** 
The ESP8266, Touch sensors, and the USB Serial converter requires a stable 3.3V supply with a enough current to handle short current peaks. 

---

## Microcontroller Selection

### ESP8266
**Descision:** The ESP8266 is selected as the primary microcontroller.

**Reasoning:**
4 different microcontrollers were taken into consideration for this project. The selection criteria priotizes cost, ease of integration, and the microcontroller ecosystem.

| Criteria                  | Weight (%) | ESP32  | ESP8266 | ATmega328P | STM32L |
| ------------------------- | ---------- | ------ | ------- | ---------- | ------ |
| Power Consumption         | 10%        | 3      | 2       | 5          | 4      |
| Cost                      | 25%        | 3      | 5       | 4          | 4      |
| Ease of Programming       | 15%        | 5      | 4       | 4          | 2      |
| Long-term Scalability     | 10%        | 5      | 4       | 2          | 4      |
| PCB Integration           | 20%        | 4      | 4       | 5          | 2      |
| Microcontroller Ecosystem | 20%        | 5      | 5       | 3          | 2      |
| Weighted Total:           | 100%       | 4.1    | 4.25    | 3.9        | 2.9    |

**Notes:**
- The ESP Microcontroller line was heavily recommended due to its simplicity and its low cost. Furthermore I have some experience with the ESP32 from participating in the ASU Formula SAE team. 
- The ESP8266 was chosen over the ESP32 because of its cheaper price while still meeting the functional and preformance requirments. 

---

## LED Control

### LED Strip

**Decision:** WS2812 (NeoPixel) addressable RGB LEDs

**Reasoning:**
- RGB capabilities that allows for specific colors
- Widely supported libraries and documentation

### Logic Level Shifting

**Decision:** SN74LV1T34QDBVRQ1 single buffer is used for LED data signaling

**Reasoning:**
The ESP8266 outputs 3.3V logic levels, while the NeoPixel LEDs requires a reliable 5V logic-level data signal. The initial logic shifter used was a SN74AHCT125 quad buffer which was chosen because it was readily avaliable for a physical prototype. Only one of the input and output pins out of the 4 possible pins was being used so for the goal of simplicity the SN74LV1T34QDBVRQ1 single buffer was chosen instead. 

---

## Touch Sensors

## Capacitive Touch Controller

**Decision:** FDC1004QDGSRQ1 used for capactive touch sensing

**Reasoning:**
- Supports multiple independent electrodes 
- Proven performance for touch detection through non-conductive materials

**Notes:**
- Due to the limitations of manufactoring the MPR121 could not be used. 
---

## USB Interface

### USB to ESP8266 Communication

**Decision:** CH340C USB serial converter 

**Reasoning:**
- No external crystal required

---

## Mechanical Design

### PCB Design

**Decision:** Custom PCB designed in KiCAD

**Reasoning:**
A custom PCB reduces wiring complexity and allows slim and small profile for the electronics

---

## TODO
- Finalize PCB Layout
- Firmware development and integration for the ESP8266
- Solidworks model for the pcb enclosure and mirror design
