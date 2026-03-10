# smart-vanity-mirror

Custom built ESP8266 based smart vanity mirror with touch controls, USB-C power and programming integration, custom CADed frame and custom PCB.

## Features

- Adustable LEDs brightness and color
- Touch Sensor Controls
- Custom Built Housing
- USB C Port for Power and Programming

## Hardware Overview

What this shows:
USB-C Programmer and Power Supply, Voltage Regulation, ESP8266 Microcontroller, Touch Input Circuit, LED Output Stage

![Electrical Schematic](/Docs/Images/VMP_Electrical_Schematic.jpg)

### USB-C and USB to Serial Port

The system is powered and programmed through a USB-C connector supplying 5 V and a CH340C USB to Serial UART converter.

Key design elements:
- VBUS provides 5 V input.
- CC resistors are used to negotiate default USB power mode.
- The CH340C communicates with the ESP8266 when the USB C is connected to a computer. 
- GPIO 0 boot mode circuitry and Reset circuitry
- A polyfuse is used as overcurrent protection.

### Voltage Regulation

The ESP8266 operates at 3.3 V, so a voltage regulator steps down 5 V from USB-C to 3.3 V.

Key design elements:
- 5V to 3.3V Buck Converter

### ESP8266 Microcontroller

The ESP8266 serves as the main controller for, handling touch input, driving LED outputs, and managing firmware logic

Key design elements:
- Proper decoupling capacitors near VCC
- EN (enable) pull-up resistor
- Manual Reset Switch

### Touch Input Circuit

The FDC1004-Q1 is a 4-Channel Capacitance-to-Digital Converter which is used to detect when the user touches metal pads. This data is sent to the ESP8266 to control the lights

<!-- Future Improvements

Facial recognition lighting presets

Mobile app control

Ambient light auto-adjustment

Bluetooth speaker integration -->




