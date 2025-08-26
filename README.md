# Smart Wearable System for Real-Time Hazard Detection in Industrial Environments

## **Table of Contents**

- Overview
- Key Features
- System Architecture
- Pin Map
- Quick Start (Simulation)
- Quick Start (Hardware)
- Repo Structure
- License & Acknowledgments

---

## **Overview**

This project delivers a **smart wearable system**  that performs **on‑device inference** to detect:

- **Falls**
- **Heat stress**
- **Hazardous gas spikes**

All decisions are made **on the edge** (ESP32) for **low latency**, **privacy**, and **reliability**. Telemetry and alerts stream to a backend via **MQTT** for remote monitoring.

**Development mode:** The system is fully reproducible in **Wokwi** (no hardware needed).

**Deployment mode:** Same code runs on real ESP32 hardware.

---

## **Key Features**

- **Multi‑hazard sensing:** MQ‑135 (gas), DHT22 (temp/humidity), MPU6050 (IMU).
- **Edge AI:** TinyML fall classifier (Edge Impulse) + **physics fallback** (free‑fall/spike logic).
- **Predictive pre‑warn:** Trend buffers provide **early warnings** before thresholds are crossed.
- **Local alerts:** Buzzer + LED.
- **MQTT streaming:** JSON status to HiveMQ topic for dashboards.

---

## **System Architecture**

- **Sensing:** DHT22, MQ‑135, MPU6050 .
- **Processing:** ESP32 runs TinyML classifier + rule-based logic.
- **Alerting:** Local (buzzer/LED) + remote (MQTT).
- **Data model:** Structured JSON with sensor values, status, and confidence.

<img width="832" height="722" alt="image" src="https://github.com/user-attachments/assets/85eacdc9-ada5-46eb-b598-fa37e98f93a9" />


---

## **Pin Map**

**Pins (default):**

```
// Digital / Analog
#define DHT_PIN        15
#define GAS_SENSOR_PIN 34   
#define ALERT_LED_PIN  25
#define BUZZER_PIN     26

// I2C (MPU6050)
SDA -> 21
SCL -> 22
```

<img width="885" height="467" alt="Circuit Diagram  - Simlation Setup" src="https://github.com/user-attachments/assets/840504c1-f840-41ae-a329-4acd1069dc41" />


**Thresholds:**

```
TEMPERATURE_THRESHOLD = 40.0   // °C
GAS_THRESHOLD         = 800.0  // ppm 
CONFIDENCE_THRESHOLD  = 0.70   // TinyML classification
```

---

## **Quick Start (Simulation)**

### **1) Clone**

```
git clone https://github.com/naveenprasathk2/IoT_Project_EEN1061_naveenprasathkanakaraj_A00048217.git
cd IoT_Project_EEN1061_naveenprasathkanakaraj_A00048217
```

### **2) Open in VS Code (PlatformIO)**

- Open folder → PlatformIO auto‑installs libs per platformio.ini.

### **3) Run Wokwi**

- Start the Wokwi simulator from PlatformIO (project includes diagram.json).

---

## **Quick Start (Hardware)**

1. Wire modules per **Pin Map** above.
2. Build & flash with **PlatformIO** (ESP32 dev platform).
3. Open Serial Monitor @ **115200**.
4. Ensure Wi‑Fi SSID/password are set:

```
const char* ssid = "Wokwi-GUEST";
const char* password = "";
```

5. Subscribe to MQTT in HiveMQ:

- **Broker:** broker.hivemq.com:1883
- **Topic:** SafetySystem/A00048217/safety_data

---

## **Repo Structure**

```
├── src/
│   ├── main.cpp                            # Main application code
│   └── motion-detection_inferencing/       # Edge Impulse TinyML library
├── wokwi/
│   └── diagram.json                        # Simulation circuit
├── docs/
│   ├── circuit_diagram.png                 # Simulation setup diagram
│   ├── system_architecture.jpg             # System architecture
│   └── testing_evaluation.xlsx             # Test matrix & results
│ 
└── README.md                               # Documentation
```

---

## **License & Acknowledgments**

**Author:** *Naveen Prasath Kanakaraj* (A00048217), Dublin City University.

**Thanks:** Edge Impulse, Wokwi, PlatformIO, HiveMQ.
