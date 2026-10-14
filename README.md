ESP32 Distributed IoT System

Wireless Sensor Network | ESP-NOW | Automated Control | Power Optimization

Project Overview

An ESP32-based distributed IoT prototype designed to demonstrate wireless communication, environmental monitoring, automated control, and energy-efficient embedded system operation.

The project uses two ESP32 microcontrollers, each responsible for a specific part of the system.

Rather than relying on a single microcontroller for every operation, the architecture separates data acquisition from processing and actuator control.

This project was developed as a practical application of concepts explored during the Advanced ESP32 IoT Training Program.

System Architecture

Sensor Node (ESP32)

DHT11 + LDR
↓
Sensor Data Acquisition
↓
ESP-NOW Wireless Transmission
↓
Gateway Node (ESP32)
↓
Data Processing & Decision Making
↓
LED & Relay-Controlled DC Motor

Communication: ESP-NOW, Channel 11

The gateway also connects to Wi-Fi, providing a foundation for future MQTT and cloud integration.

Key Features

1. Wireless Communication

- ESP-NOW peer-to-peer communication.
- Lightweight binary data packets.
- Dedicated Sensor Node and Gateway architecture.
- Transmission status monitoring.

2. Environmental Monitoring

- Temperature measurement using DHT11.
- Humidity measurement using DHT11.
- Ambient light monitoring using an LDR.
- Sensor reading validation.

3. Automated Control

- Temperature-based DC motor control through a relay.
- Light-dependent LED control.
- Temperature hysteresis to reduce frequent motor switching.

4. Power Management

- ESP32 Deep Sleep on the Sensor Node.
- Automatic wake-up using a timer.
- Periodic sensor readings and data transmission.
- Gateway CPU frequency reduced to 80 MHz.
- Wi-Fi power-saving mode enabled on the Gateway.

Hardware Components

Component| Purpose
ESP32 DevKit × 2| Sensor and Gateway
DHT11| Temperature and humidity
LDR| Light sensing
Relay Module| DC motor switching
DC Motor| Temperature-based actuation
LED| Light-dependent indication
Breadboard & Jumper Wires| Circuit prototyping

Pin Configuration

Sensor Node

Component| ESP32 GPIO
DHT11| GPIO 4
LDR| GPIO 34

Gateway Node

Component| ESP32 GPIO
LED| GPIO 26
Relay| GPIO 27

The relay configuration uses active-low switching.

Control Logic

Temperature-Based Motor Control

- Temperature ≥ 27°C → Motor ON
- Temperature ≤ 25.5°C → Motor OFF
- Between 25.5°C and 27°C → Previous motor state maintained

This hysteresis prevents unnecessary switching around a single temperature threshold.

Light-Based LED Control

- LDR ADC value > 2500 → LED ON
- LDR ADC value ≤ 2500 → LED OFF

These thresholds were selected based on the behavior of the sensors used during prototyping.

Sensor Node Workflow

1. ESP32 wakes from Deep Sleep.
2. Initializes the DHT11 and LDR.
3. Collects environmental readings.
4. Creates an ESP-NOW data packet.
5. Sends the packet to the Gateway.
6. Waits for transmission status.
7. Enters Deep Sleep for 10 seconds.
8. Repeats the cycle after waking.

Gateway Workflow

1. Initializes the LED and relay outputs.
2. Connects to the configured Wi-Fi network.
3. Checks that the Wi-Fi channel matches the ESP-NOW channel.
4. Initializes ESP-NOW communication.
5. Receives sensor data packets.
6. Validates packet size and sensor status.
7. Applies temperature and light control logic.
8. Updates actuator states.

The Gateway remains awake to receive incoming sensor data.

Software & Technologies

- C++ / Arduino Framework
- ESP32 Arduino Core 3.x APIs
- ESP-NOW
- Wi-Fi
- Deep Sleep & Timer Wake-up
- Embedded Sensor Interfacing
- Automated Control Logic
- Serial Monitoring & Debugging

Repository Structure

Gateway/ — Gateway firmware

Sensor_Node/ — Sensor Node firmware

README.md — Project documentation

.gitignore — Git exclusion rules

Setup Instructions

1. Install the ESP32 board package in Arduino IDE.
2. Install the required DHT sensor library.
3. Configure the Gateway Wi-Fi credentials.
4. Ensure the Gateway Wi-Fi channel matches the Sensor Node ESP-NOW channel.
5. Update the Sensor Node with the Gateway's Wi-Fi MAC address.
6. Connect the hardware according to the pin configuration.
7. Upload the corresponding firmware to each ESP32.
8. Use the Serial Monitor at 115200 baud to observe operation.

Note: Never publish real Wi-Fi passwords or other private credentials.

Current Scope & Limitations

This project is an educational prototype focused on implementing and integrating embedded IoT concepts.

- The battery percentage is currently a placeholder, not a measured value.
- The transmitted RSSI field is also a placeholder.
- ESP-NOW packet encryption is not enabled.
- MQTT, OTA updates, and TinyML are not implemented in this version.
- Further testing and reliability improvements are required before real-world deployment.

Future Improvements

- Secure MQTT communication and cloud integration.
- Over-the-Air firmware updates.
- ESP-NOW security enhancements.
- Real battery voltage monitoring.
- Improved packet handling and communication recovery.
- FreeRTOS-based task management.
- Edge AI integration for intelligent monitoring.

Project Purpose

The objective of this project was not to build a large-scale commercial solution, but to apply advanced IoT concepts within a practical distributed embedded system.

It also provides a foundation for future development toward more reliable, secure, efficient, and intelligent connected systems.

---

Developed as part of an ongoing learning journey in Embedded Systems and IoT Engineering.
