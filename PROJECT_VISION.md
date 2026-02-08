# VayuNode: Project Vision & Technical Strategy

**Document Status:** Draft 1.0  
**Authored By:** Product Lead & Lead Systems Engineer  
**Date:** February 2026

---

## 1. Hardware-Software Synergy: The Intelligent Edge
VayuNode is not a passive data logger; it is an intelligent edge device. Our architecture leverages the synergy between high-performance microcontrollers and AI-enabled sensing to minimize bandwidth while maximizing insight.

### The Core: Pico 2W + BME688
*   **Edge-AI Processing**: We utilize the Raspberry Pi Pico 2W's dual-core RP2040 to run the **Bosch BSEC 2.x library** locally. Instead of sending raw resistance values to the cloud, the device processes gas patterns *on-edge*.
    *   *Scenario*: The device can distinguish between a "Coffee Shop Smell" (benign VOCs) and "Traffic Exhaust" (harmful NOx/CO) based on gas signatures, sending only the context-aware Air Quality Index (IAQ) via NB-IoT.
*   **Connectivity**: NB-IoT (Narrowband IoT) is chosen for its deep indoor penetration and low power consumption, ensuring nodes work in basements or rural areas where Wi-Fi is absent.

### Public Visibility: HUB75 P10 Display
Air quality data belongs to the public, not just the app user.
*   **Logic**: The 32x16 RGB LED Matrix acts as a "Public Traffic Light" for air quality.
*   **Visual Distance**: Calibrated for 50-meter visibility.
    *   **Green (IAQ 0-50)**: Safe.
    *   **Yellow (IAQ 51-100)**: Moderate.
    *   **Red (IAQ 100+)**: Hazardous – Visible warning for joggers/pedestrians.

## 2. User Integration & Customization
We serve two distinct user personas: the Concerned Citizen and the Data Scientist.

### Personalized Dashboards
The VayuCloud platform offers a toggle-able interface:
*   **"Simple Mode" (Default)**: Shows a large, color-coded AQI number and a health recommendation (e.g., "Good for outdoor exercise").
*   **"Expert Mode"**: Unlocks raw telemetry:
    *   VOC (Volatile Organic Compounds) in ppb.
    *   eCO2 (estimated Carbon Dioxide) in ppm.
    *   Barometric Pressure & Humidity trends.

### Community Grouping: "Local Mesh"
*   **Feature**: Users can form a "Neighbourhood Watch" for air.
*   **Implementation**: A resident in Kerala can create a "Kochi-MG-Road-Mesh" group. Aggregated data from 5-10 nodes creates a hyper-local pollution map, allowing the community to track how a smoke plume moves across the neighborhood in real-time.

## 3. Open Data & Global Integration
VayuNode is an Open Source Hardware (OSHW) project committed to Open Data.

### OpenStreetMap (OSM) Integration
*   **Live Overlay**: Every public VayuNode is effectively a pixel on a global heat map. We overlay live AQI gradients onto OpenStreetMap, providing an alternative to proprietary counterparts like Google Maps Air Quality.

### Data Democratization
*   **Export Tools**: A "Download Data" API allows:
    *   **Researchers**: To fetch bulk CSV/JSON logs for climate studies.
    *   **Local Government**: To access verified historical trends for urban planning policy.

## 4. The MVP Mobile App (IAIQ Dashboard)
The mobile app is the primary interface for device setup and alerts.

### Design Philosophy
*   **Aesthetic**: "Industrial AI" – Dark mode, high contrast (Neon Cyan/Amber data points), minimal clutter.

### Key Features
1.  **Scan-to-Connect**: QR code provisioning. The app passes Wi-Fi/NB-IoT credentials to the Pico 2W via Bluetooth Low Energy (BLE) during initial setup.
2.  **Push Alerts**:
    *   *Safety*: "High VOC Detected (Paint/Smoke) - Open Windows."
    *   *Maintenance*: "Sensor Heater Verification Failed" or "Check Power Supply."
3.  **Node Health**: Real-time heartbeat monitoring (Signal Strength, Uptime).

## 5. Post-Hardware Scaling (The Expansion)
Hardware is hard; documentation makes it scalable.

### The VayuNode Wiki
We will maintain a "Living Manual" on GitHub Wiki:
*   **Assembly Guides**: Step-by-step video & CAD renders for assembling the kit.
*   **KiCad Files**: Fully open-source PCB schematics (Gerber files) for local manufacturing.
*   **Firmware**: MicroPython libraries for BME688 and HUB75 driver optimization.

### Phase 2 Features
*   **Solar Integration**: A dedicated PMIC (Power Management IC) add-on board for off-grid deployment on streetlights.
*   **LoRaWAN Fallback**: A drop-in replacement for the NB-IoT module, enabling long-range communication for forestry/agricultural monitoring in the Western Ghats.
