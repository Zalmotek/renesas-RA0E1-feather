# Zalmotek RA0E1 Feather USB Serial

A UART communication example for the Zalmotek RA0E1 Feather development board, powered by Renesas.

## Overview

This project demonstrates UART serial communication on the Zalmotek RA0E1 Feather board. The program initializes the UARTA peripheral and provides an Arduino-compatible Serial API for easy serial communication. It includes a demo that blinks an LED while sending status messages ("LOW"/"HIGH") over USB serial at 115200 baud.

## Hardware Requirements

- Zalmotek RA0E1 Feather board
- USB connection for programming and serial communication

## Software Requirements

- e2 studio IDE
- Renesas FSP (Flexible Software Package)
- J-Link Debug Probe
- Serial terminal application (e.g., PuTTY, TeraTerm, Arduino Serial Monitor)

## Features

- Arduino-compatible Serial API (Serial.begin, Serial.print, Serial.println, Serial.read, etc.)
- Dual UART channel support (Serial and Serial1)
- Configurable baud rate
- LED blink demonstration with serial output
- Interrupt-driven receive with 512-byte buffer

## Code Functionality

The main application:
- Initializes UART communication at 115200 baud using `Serial.begin(115200)`
- Toggles the LED on Pin P102 (BSP_IO_PORT_01_PIN_02)
- Outputs "LOW" and "HIGH" messages via USB serial during LED state changes
- Implements timing delays of 300ms for LOW state and 1000ms for HIGH state

The SerialCompatibilityLayer provides:
- `begin(baud)` - Initialize UART with specified baud rate
- `print(msg)` / `println(msg)` - Send strings or numbers
- `write(byte)` - Send a single byte
- `available()` - Check if data is available to read
- `read()` - Read a byte from the buffer
- `peek()` - Look at the next byte without removing it

## Getting Started

### Setup

1. Clone this repository
2. Open the project in e2 studio
   In e² studio go to File -> Import..., choose "Existing Projects into Workspace" and browse to the project you've just downloaded, then click Finish:

<p align="center">
  <img src="../../Blink/Ra0E1_Feather_Blink/1.png" height="500">
  <img src="../../Blink/Ra0E1_Feather_Blink/2.png" height="500">
</p>

After importing your project, open the configuration.xml file to access the board configurator. Let's review some key settings that will be relevant for all your future RA0E1 Feather SoM projects. First of all, in the BSP tab, your project should have the Custom User Board and the R7FA0E1073CFJ device selected.

<p align="center">
  <img src="../../Blink/Ra0E1_Feather_Blink/3.png" height="500">
</p>

In the Pins tab, you can configure the UART pins and GPIO. For this project:
- **P102** is set to Output Mode for the LED
- **UARTA0** is configured for serial communication (TXD0 and RXD0 pins)

You can find the LED configuration in Pin Selection menu -> Ports -> P1 -> P102. The UART configuration is under Peripherals -> Connectivity -> UARTA0.

3. Connect your Zalmotek RA0E1 Feather board via USB
4. Build the project
5. Flash the firmware to the board

To run the project, click Generate Project Content, and then you can Build the project and Debug it. In the prompt that pops up, choose Debug as Renesas GDB Hardware Debugging. Click the Resume icon to begin executing the project.

### Viewing Serial Output

After flashing and running the project, open a serial terminal application:

1. Find the COM port assigned to your RA0E1 Feather board
   - On Windows: Check Device Manager -> Ports (COM & LPT)
   - On Linux: Check `/dev/ttyACM*` or `/dev/ttyUSB*`
   - On macOS: Check `/dev/tty.usbmodem*`

2. Configure the terminal:
   - **Baud rate:** 115200
   - **Data bits:** 8
   - **Stop bits:** 1
   - **Parity:** None
   - **Flow control:** None

3. Connect and you should see "LOW" and "HIGH" messages alternating as the LED blinks.

### Configuration

The baud rate can be adjusted by modifying the `Serial.begin()` call in `hal_entry.cpp`:

```c
Serial.begin(115200); // Change to desired baud rate
```

The blink timing can be adjusted by modifying the delay values:

```c
delay(300);  // Time LED stays LOW (milliseconds)
delay(1000); // Time LED stays HIGH (milliseconds)
```

## Serial API Usage Examples

### Sending Data

```c
Serial.begin(115200);

// Print strings
Serial.print((uint8_t*)"Hello ");
Serial.println((uint8_t*)"World!");  // Adds newline

// Print numbers
Serial.print(42);
Serial.println(-123);

// Write single byte
Serial.write(0x55);
```

### Receiving Data

```c
Serial.begin(115200);

while (true) {
    if (Serial.available() > 0) {
        uint8_t byte = Serial.read();
        // Process received byte
        Serial.write(byte);  // Echo back
    }
}
```

## Project Structure

- `src/hal_entry.cpp`: Main application code with LED blink and serial demo
- `src/SerialCompatibility.h`: Header defining the Arduino-compatible Serial API
- `src/SerialCompatibility.cpp`: Implementation of the Serial compatibility layer
- `configuration.xml`: FSP project configuration

## License

This project is provided for educational purposes.

## Additional Resources

- [Zalmotek Website](https://zalmotek.com)
- [Zalmotek RA0E1 Website](https://zalmotek.com/products/RA0E1-Feather-SoM/)
- [FSP Documentation](https://www.renesas.com/us/en/software-tool/flexible-software-package-fsp)
