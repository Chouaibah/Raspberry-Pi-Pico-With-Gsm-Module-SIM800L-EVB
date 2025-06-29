# Raspberry Pi Pico with GSM Module (SIM800L EVB)

A MicroPython-based project that demonstrates how to interface a Raspberry Pi Pico with a SIM800L EVB GSM module over UART to send data upon receiving a phone call.

---

## Table of Contents

- [Overview](#overview)  
- [Features](#features)  
- [Hardware Requirements](#hardware-requirements)  
- [Software Requirements](#software-requirements)  
- [Wiring Diagram](#wiring-diagram)  
- [Installation](#installation)  
- [Usage](#usage)  
- [Troubleshooting](#troubleshooting)  
- [Contributing](#contributing)  
- [License](#license)  

---

## Overview

This repository contains example code and instructions for using a Raspberry Pi Pico to communicate with a SIM800L EVB GSM module via AT commands in MicroPython. The primary goal is to detect an incoming call and then transmit collected data (e.g., sensor readings or status messages) back over the cellular network.

---

## Features

- Initialize and configure the SIM800L EVB module  
- Detect incoming calls  
- Send data (SMS or HTTP GET/POST) when a call is received  
- Read, delete, and manage SMS messages  
- Basic HTTP functionality over GPRS  

---

## Hardware Requirements

- **Raspberry Pi Pico** (with MicroPython UF2 firmware installed)  
- **SIM800L EVB GSM module**  
- **5 V, 1–2 A power supply** for the SIM800L (to handle transmission peaks)  
- **Jumper wires** for UART connections  
- (Optional) Breadboard or PCB for stable mounting  

---

## Software Requirements

- [Thonny IDE](https://thonny.org/) or another MicroPython-compatible editor  
- MicroPython firmware on the Pico (download the latest UF2 from the Raspberry Pi website)  
- (Optional) `rshell` or `ampy` for copying files to the Pico  

---

## Wiring Diagram

![reel_montage](https://github.com/Chouaibah/Chouaibah/assets/158000674/064e16bf-dff2-458a-a08c-f8b2b1036633)


> **Note:** Do **not** power the SIM800L from the Pico’s 3.3 V rail—use a dedicated 5 V, high-current supply.

---

## Installation

1. **Flash MicroPython**  
   - Download the Pico UF2 from https://www.raspberrypi.org/documentation/microcontrollers/micropython.html  
   - Hold the BOOTSEL button on your Pico while plugging it in, then drag-and-drop the UF2 file.  

2. **Copy the Code**  
   - Clone this repo or download `main.py` and any supporting modules (e.g., `sim800l.py`).  
   - Use Thonny or `rshell`/`ampy` to upload files to the Pico’s root directory.  

3. **Configure Serial Console**  
   - If using a Raspberry Pi host, disable the serial console on `/dev/serial0` via `raspi-config`  
   - Otherwise, ensure no other application is holding the UART port.  

---

## Usage

1. **Power On**  
   - Connect the Pico and SIM800L to their power sources and wiring as shown above.  

2. **Run the Script**  
   - Open the REPL in Thonny or a terminal, then execute:
      ```python
      import main
      main.run()
      ```
   - The script will initialize the SIM800L, wait for an incoming call, then send your predefined data.

3. **Customize Your Data**  
   - Edit `main.py` to change the phone number, message content, or to switch from SMS to HTTP.  
   - Set your APN credentials in the `setup_gprs()` function if you plan to use HTTP.  

---

## Troubleshooting

- **No Network Registration**  
  - Verify your SIM card is active and the provider still supports 2G.  
  - Check signal strength with `AT+CSQ`.  

- **Power-Related Resets**  
  - Use a beefy 5 V, 2 A supply; voltage dips during transmission can cause reboots.  

- **UART Errors**  
  - Confirm TX/RX lines are crossed correctly (Pico TX → SIM RX, Pico RX ← SIM TX).  
  - Match baud rates (default 115200).  

---

## Contributing

1. Fork the repository  
2. Create a feature branch (`git checkout -b feature/YourFeature`)  
3. Commit your changes (`git commit -m "Add feature"`)  
4. Push to your branch (`git push origin feature/YourFeature`)  
5. Open a Pull Request describing your changes  

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
