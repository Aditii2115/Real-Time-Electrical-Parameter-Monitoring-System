# Real-Time-Electrical-Parameter-Monitoring-System
## Overview

This project presents a simple, low-cost, real-time electrical parameter monitoring system built using the **ESP32 microcontroller** and the **PZEM004T energy monitoring module**. The system measures key electrical parameters — **voltage, current, power, and power factor** — of a connected AC load and displays them in real time on a **16×2 I2C LCD**, without relying on cloud platforms, Wi-Fi dashboards, or external infrastructure.

Traditional electrical monitoring systems are often bulky, expensive, and require manual observation using analog instruments like voltmeters and ammeters. This project addresses that gap by offering a compact, standalone, and accurate embedded solution suitable for educational use and small-scale industrial/domestic monitoring.

## Features

- Real-time measurement of **voltage, current, power, and power factor**
- Local display on a **16×2 LCD** via I2C (no cloud/app dependency)
- Uses a **current transformer (CT)** for safe, isolated current sensing
- Simple **UART-based serial communication** between ESP32 and PZEM004T
- Periodic, continuously updated readings
- Compact and cost-effective — ideal for labs, coursework, and small-scale applications

## Hardware Components

| Component | Purpose |
|---|---|
| ESP32 Microcontroller | Main processing unit; reads data from PZEM004T and drives the LCD |
| PZEM004T Module | Measures voltage, current, power, and power factor |
| Current Transformer (CT) | Senses load current with electrical isolation from the high-voltage line |
| 16×2 LCD (I2C) | Displays real-time readings |
| Electrical Load (Filament Bulb) | Used as a test load to validate the system |

## How It Works

1. The **PZEM004T** module measures the supply voltage directly and senses current through the **CT**.
2. It calculates real power and power factor internally and sends the data to the **ESP32** via UART (9600 bps).
3. The ESP32 processes the received values and displays voltage, current, power, and power factor on the **I2C LCD**, updating the readings periodically.

```
AC Mains + Bulb → PZEM004T (+ CT) → ESP32 (UART) → 16×2 I2C LCD
```

## System Architecture

```
[AC Mains] → [PZEM004T + CT] --Serial(UART)--> [ESP32] --I2C--> [16x2 LCD]
                     ↑
                  [Bulb Load]
```

## Results

The system was tested using a filament bulb as the load, yielding the following readings:

| Parameter | Value |
|---|---|
| Voltage | 241.0 V |
| Current | 0.45 A |
| Power | 108 W |
| Power Factor | 1.00 |

Since a filament bulb behaves as a purely resistive load, the power factor was close to unity, confirming accurate measurement.

## Code

The firmware (Arduino/ESP32 sketch) is included in this repository. It:
- Initializes the LCD and PZEM004T communication
- Continuously reads voltage, current, power, and power factor from the PZEM004T
- Displays the readings on the LCD every 4 seconds
- Logs values to the Serial Monitor for debugging

### Libraries Used

- `PZEM004Tv30.h` — for communication with the PZEM004T module
- `LiquidCrystal_I2C.h` — for driving the 16×2 I2C LCD
- `WiFi.h` — (optional, used for future IoT expansion)

## Applications

- Educational demonstrations of embedded energy monitoring
- Small-scale industrial or domestic power monitoring
- Base platform for future IoT-based energy monitoring systems (data logging, remote monitoring, etc.)

## Future Scope

- Add Wi-Fi-based remote monitoring/dashboard
- Data logging to cloud or SD card
- Integration with mobile apps for historical analysis
- Support for multiple loads/multi-channel monitoring

