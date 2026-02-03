# Zalmotek RA0E1 Feather SoM 

Welcome to the <a href="https://zalmotek.com/products/RA0E1-Feather-SoM/">Zalmotek RA0E1 Feather SoM</a> GitHub repository!

Here you'll find all the resources you need to get up and running quickly.

## 🪶 What is the RA0E1 Feather SoM?

The <a href="https://www.renesas.com/en/products/microcontrollers-microprocessors/ra-cortex-m-mcus/ra0e1-32mhz-arm-cortex-m23-entry-level-ultra-low-power-general-purpose-microcontroller">Renesas RA0E1</a> Microcontroller is designed for ultra-low power applications, featuring the Arm® Cortex®-M23 CPU core with a maximum operating frequency of 32 MHz. It's ideal for IoT devices and battery-powered applications requiring extended operation times.

The Feather SoM incorporates the classic Feather features: GPIOs (analog and digital), I2C and SPI communication pins, UART pins, a LiPo battery power plug, and the USB programming port. The SoM also features a USB Type-C for powering the board and for USB debug upload, making it perfect for portable and low-power projects.

## Pinout Overview

The Feather has two headers:
- **Left Header**: 16-pin (power, analog, SPI, UART)
- **Right Header**: 12-pin (power, digital GPIO, I2C)

### Left Header (16-pin)

| Pin # | Feather Pin | MCU Pin | Function | Description |
|-------|-------------|---------|----------|-------------|
| 1 | RST | nRESET | Reset | Active-low reset |
| 2 | 3V3 | - | Power | 3.3V regulated output |
| 3 | AREF | AREF | Analog | Analog reference voltage |
| 4 | GND | - | Power | Ground |
| 5 | A0 | P015 | Analog | ADC input |
| 6 | A1 | P014 | Analog | ADC input |
| 7 | A2 | P013 | Analog | ADC input |
| 8 | A3 | P012 | Analog | ADC input |
| 9 | A4 | P009 | Analog | ADC input |
| 10 | A5 | P008 | Analog | ADC input |
| 11 | SCK | P112 | SPI | SPI clock |
| 12 | MOSI | P109 | SPI | SPI data out (Microcontroller Out) |
| 13 | MISO | P110 | SPI | SPI data in (Microcontroller In) |
| 14 | RX | P100 | UART | UART receive |
| 15 | TX | P101 | UART | UART transmit |
| 16 | SPARE | P215 | GPIO | Spare GPIO |

### Right Header (12-pin)

| Pin # | Feather Pin | MCU Pin | Function | Description |
|-------|-------------|---------|----------|-------------|
| 1 | BAT | - | Power | LiPo battery input (3.0-4.2V) |
| 2 | EN | PWR_EN | Control | Enable pin - pull low to disable 3.3V regulator |
| 3 | USB | - | Power | USB VBUS (5V) |
| 4 | D0 | P407 | GPIO | Digital I/O |
| 5 | D1 | P201 | GPIO | Digital I/O |
| 6 | D2 | P200 | GPIO | Digital I/O |
| 7 | D3 | P300 | GPIO/SWD | Digital I/O / SWCLK |
| 8 | D4 | P108 | GPIO/SWD | Digital I/O / SWDIO |
| 9 | D5 | P103 | GPIO | Digital I/O |
| 10 | D6 | P102 | GPIO | Digital I/O |
| 11 | SCL | P914 | I2C | I2C clock |
| 12 | SDA | P913 | I2C | I2C data |

### Power Pins

| Pin | Voltage | Description |
|-----|---------|-------------|
| 3V3 | 3.3V | Regulated 3.3V output from ISL9120 buck converter |
| USB | 5V | USB VBUS power input (4.5-5.5V) |
| BAT | 3.0-4.2V | LiPo battery input via JST PH connector |
| GND | 0V | Common ground |
| EN | - | Active-high enable for 3.3V regulator (pulled high by default) |

### Special Functions

#### SWD Debug Interface
The SWD debug connector is directly connected to:
- **SWDIO**: P108 (shared with D4)
- **SWCLK**: P300 (shared with D3)
- **nRESET**: Reset pin

#### UART Interfaces
The board has two UART interfaces:
1. **Feather UART** (P100/P101): Available on header pins RX/TX
2. **FTDI UART** (P207/P208): Connected to USB-UART bridge (FT231X)

#### Additional Features
- **User LED**: Connected to P214 (active-high, green)
- **Reset Button**: Connected to nRESET
- **Battery Charger**: ISL9205 for LiPo charging via USB

## 🐣🏁 Quick Start Guide

### 🔌 Hardware Requirements
- USB-C cable
- JTAG Degugger, such as the <a href="https://www.segger.com/products/debug-probes/j-link/">SEGGER J-Link</a>

### 💻 Development Environment Setup

#### Installing Renesas e² studio IDE

The e² studio IDE from Renesas is a comprehensive, user-friendly platform designed to streamline embedded application development. It supports Renesas microcontrollers and combines powerful features with an intuitive interface for coding, debugging, and project management.

First of all, download the latest release of the Flexible Software Package with the e²studio platform installer from the following <a href="https://www.renesas.com/us/en/software-tool/e2studio-information-ra-family">link</a>, according to your OS.

The installer will guide you through the necessary steps. After the installation is finished, launch Renesas e² studio and set up your workspace. This will be the directory where all your projects will be stored.

You will also need to install the J-Link Software pack from <a href="https://www.segger.com/products/debug-probes/j-link/technology/flash-download/">here</a>.

#### Running your first project

Once you have all the tools installed, follow <a href="https://github.com/Zalmotek/zalmotek-RA0E1-feather/tree/diode-RA0E1-feather-rev1.0.0/firmware/UART/Ra0E1_Feather_USB_Serial">this</a> guide to learn how to import, build, and run a project in the e² studio IDE. 

---
Thank you for choosing the Zalmotek RA0E1 Feather SoM! 

We can't wait to see what amazing projects you'll create with it! 💻✨
