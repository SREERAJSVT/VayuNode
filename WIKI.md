# VayuNode Wiki

Welcome to the **VayuNode** knowledge base. This wiki documents the open-source hardware, firmware, and data protocols for the Silicon Sahyadri air quality network.

> **Philosophy**: "If it doesn't work on the bench, it won't work in the monsoon." We code for reliability and document for the community.

---

## 📚 Quick Links
- **[Project Vision](PROJECT_VISION.md)**: The technical strategy and future roadmap.
- **[Roadmap](ROADMAP.md)**: Current development phase and milestones.
- **[GitHub Repository](https://github.com/silicon-sahyadri/VayuNode)**: Source code and issue tracking.
- **[Discord Community](https://discord.gg/QSC84jYQ)**: Join the #vayu-node channel for live support.

---

## 🛠️ Hardware Guide (Phase 1: Breadboard MVP)

### Bill of Materials (BoM)
| Component | Function | Notes |
| :--- | :--- | :--- |
| **Raspberry Pi Pico 2W** | Core Controller | Dual-core RP2040 + Wi-Fi |
| **Bosch BME688** | Gas Sensor | AI-enabled VOC/eCO2 sensing |
| **HUB75 P10 Display** | Visual Output | 32x16 RGB LED Matrix (Indoor/Outdoor) |
| **SIM7000G / NB-IoT** | Connectivity | Fallback for remote areas |
| **Power Supply** | 5V 4A Adapter | Powers both Pico and hungry LED matrix |

### Wiring Diagram (Draft)
*   **BME688**: Connect via I2C (SDA -> GP8, SCL -> GP9, 3.3V, GND).
*   **HUB75 Matrix**: Requires 13 GPIO pins. (Specific pinout mapping coming in `v0.2`).
*   **NB-IoT**: UART connection (TX -> GP0, RX -> GP1).

> **⚠️ Warning**: Do NOT power the P10 LED Matrix directly from the Pico's 5V pin. Use an external 5V power supply with a common ground.

---

## 💻 Firmware Guide

### 1. Environment Setup
1.  Download the **MicroPython w/ Network Support** `.uf2` file.
2.  Hold `BOOTSEL` on Pico 2W and connect USB.
3.  Drag-and-drop the `.uf2` file to the `RPI-RP2` drive.
4.  Install **Thonny IDE** or **VS Code (Pico-W-Go)**.

### 2. Library Installation
The `vayu-lib` package (coming soon) abstracts the complex BSEC library interactions.
```python
import mip
mip.install("github:silicon-sahyadri/vayu-lib")
```

### 3. Configuration (`config.json`)
Create a root `config.json` file for your node's credentials:
```json
{
  "node_id": "VYU-KER-001",
  "wifi_ssid": "My_Home_Wifi",
  "wifi_pass": "SecretPassword",
  "mqtt_broker": "mqtt.vayunode.org",
  "lat": 9.9312,
  "lon": 76.2673
}
```

---

## 📡 Network & Data Protocol

### MQTT Topic Structure
Nodes publish data to hierarchical topics for scalable subscription:
- `vayu/{region}/{node_id}/telemetry`: JSON payload with sensor readings.
- `vayu/{region}/{node_id}/status`: Heartbeat (RSSI, Uptime).

### Payload Example
```json
{
  "ts": 167889231,
  "iaq": 45,
  "temp": 28.4,
  "hum": 62.0,
  "voc_ppb": 120,
  "source": "BME688_BSEC"
}
```

---

## 🤝 Contribution Guidelines
1.  **Fork & Branch**: Create a feature branch (`feat/new-sensor-driver`).
2.  **Test Locally**: Verify code on actual hardware if possible.
3.  **Document**: Update this Wiki if you change pinouts or APIs.
4.  **Pull Request**: Submit to `main`.
