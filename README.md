# ESP32-S3 Network Honeypot Node

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform: ESP32-S3](https://img.shields.io/badge/Platform-ESP32--S3-blue)](https://www.espressif.com/en/products/socs/esp32-s3)
[![Status: Prototype](https://img.shields.io/badge/Status-Prototype-orange)]()
[![GitHub issues](https://img.shields.io/github/issues/yourusername/esp32-honeypot-node)](https://github.com/yourusername/esp32-honeypot-node/issues)

> **A Low-Cost, Portable Deception and Attack-Capture Device for IoT Networks**

<div align="center">
  <img src="https://www.electrokit.com/upload/quick/43/2f/a461_ESP32-S3-ETH-details-size.jpg" alt="System Architecture" width="700"/>
  <p><em>ESP32-S3 Network Honeypot Node - System Architecture</em></p>
</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Hardware Requirements](#-hardware-requirements)
- [Bill of Materials](#-bill-of-materials)
- [System Architecture](#-system-architecture)
- [Schematic & Wiring](#-schematic--wiring)
- [Software Setup](#-software-setup)
- [Attack Detection](#-attack-detection)
- [Performance Results](#-performance-results)
- [Comparison with Alternatives](#-comparison-with-alternatives)
- [Quick Start](#-quick-start)
- [Testing & Validation](#-testing--validation)
- [Challenges & Lessons Learned](#-challenges--lessons-learned)
- [Future Work](#-future-work)
- [References](#-references)
- [Team](#-team)
- [License](#-license)

---

## 📖 Overview

The **ESP32-S3 Network Honeypot Node** is a compact, battery-powered device that combines **low-interaction service emulation** with **Wi-Fi frame monitoring** to lure attackers, capture their interactions, and classify common attack types on-device. Unlike traditional honeypots that run on servers or single-board computers, this node is designed for **affordable, portable edge deployment** in home and small-office networks.

### Why This Project?

- **Growing IoT Attack Surface**: Millions of IoT devices with weak default configurations are routinely scanned and recruited into botnets
- **Cost Barrier**: Existing enterprise honeypots cost $1,000+/year, making them inaccessible for small networks
- **Power Constraints**: Server-based honeypots consume significant power and cannot run unattended on battery
- **Visibility Gap**: Small networks lack affordable security monitoring solutions

### How It Works

The node operates in three parallel modes:
1. **Service Emulation**: Presents fake IoT services (Telnet, HTTP, SSH) to attract scanners
2. **Wi-Fi Sniffing**: Monitors 802.11 management frames in promiscuous mode
3. **On-Device Classification**: Labels attacks using rule-based detection

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🎯 **Service Emulation** | Fake Telnet (port 23), HTTP (port 80), and SSH-style banners |
| 📡 **Wi-Fi Frame Capture** | Monitor-mode sniffing for deauthentication and beacon floods |
| 🔍 **Port Scan Detection** | Identifies reconnaissance activity from single sources |
| 🔐 **Brute-Force Capture** | Logs failed login attempts and credential dictionaries |
| 📊 **On-Device Classification** | Rule-based detection with >94% accuracy |
| 💾 **Local Offline Logging** | microSD storage of timestamped attack records |
| 🖥️ **OLED Status Display** | Real-time IP, connection status, and attack counters |
| 🔋 **Battery Powered** | 1200mAh LiPo with protection circuitry |
| 🌐 **Cloud Dashboard** | Optional Wi-Fi uplink for alerts and aggregation |
| 💰 **Low Cost** | ~$25 total hardware cost |

---

## 🛠️ Hardware Requirements

### Recommended Hardware

| Component | Specification | Purpose |
|-----------|---------------|---------|
| **ESP32-S3** | N16R8 variant (16MB Flash, 8MB PSRAM) | Main processing unit |
| **OLED Display** | 0.96" I2C (SSD1306) | Real-time status monitoring |
| **microSD Module** | SPI interface | Local attack logging |
| **microSD Card** | 16GB or 32GB | Storage media for logs |
| **LiPo Battery** | 3.7V 1200mAh 25C | Portable power |
| **Charger Module** | TP4056 Type-C with protection | Battery management |
| **Breadboard** | MB102 | Prototyping platform |
| **Jumper Wires** | M-to-F & M-to-M mix | Connections |
| **Power Switch** | SPDT slide switch | Power control |

### Optional Components

- **Type-C Data Cable**: For firmware flashing
- **Cloud Dashboard**: ThingsBoard, Blynk, or custom solution
- **Raspberry Pi**: For attack generation during testing

---

## 💰 Bill of Materials

| ITEM | COMPONENT | UNIT PRICE (BDT) | QTY | TOTAL (BDT) | LINK |
|------|-----------|-----------------|-----|-------------|------|
| 1.0 | ESP32-S3 DevKitC-1 N16R8 | ৳1,055 | 1 | ৳1,055 | [Robotics Shop](https://www.roboticsshop.com.bd/product/esp32-s3-devkitc1-n16r8-development-board-dual-usb-type-c-hF7egZ) |
| 2.0 | 0.96" I2C OLED Display | ৳300 | 1 | ৳300 | [RoboticsBD](https://store.roboticsbd.com/internet-of-things-iot/3951-esp32-development-board-with-28-inch-tft-touch-display-robotics-bangladesh.html) |
| 3.0 | Micro SD Card Module | ৳80 | 1 | ৳80 | [RoboDocBD](https://robodocbd.com/product/microsd-card-module-for-arduino) |
| 4.0 | Micro SD Card (16GB) | ৳350 | 1 | ৳350 | Local shop / Daraz |
| 5.0 | MB102 Breadboard | ৳150 | 1 | ৳150 | - |
| 6.0 | Jumper Wires (Mix) | ৳120 | 1 | ৳120 | [RoboticsBD](https://store.roboticsbd.com/connector/2105-male-to-male-jumper-wires-40-pin-30cm-robotics-bangladesh.html) |
| 7.0 | Type-C Data Cable | ৳100 | 1 | ৳100 | Local shop |
| 8.0 | SPDT Slide Switch | ৳18 | 1 | ৳18 | [RoboticsBD](https://store.roboticsbd.com/components/2476-spdt-slide-switch-254mm-spacing-robotics-bangladesh.html) |
| 9.0 | TP4056 Charger Module | ৳50 | 1 | ৳50 | [RoboticsBD](https://store.roboticsbd.com/battery-charger/4391-ultra-small-1a-type-c-lithium-battery-charger-module-with-protection-37v42v-robotics-bangladesh.html) |
| 10.0 | 3.7V 1200mAh LiPo Battery | ৳640 | 1 | ৳640 | [RoboticsBD](https://store.roboticsbd.com/quadcopter/4494-37v-1200mah-25c-lipo-battery-robotics-bangladesh.html) |
| | | | **TOTAL** | **৳2,863 (~$25 USD)** | |

---

## 🏗️ System Architecture

### Block Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                              ESP32-S3 HONEYPOT NODE                                  │
│                                                                                      │
│  ┌──────────────────────────────────────────────────────────────────────────────┐   │
│  │                         ESP32-S3 Microcontroller                               │   │
│  │  ┌─────────────────────────────────────────────────────────────────────────┐ │   │
│  │  │                    Soft Access Point (Wi-Fi AP)                         │ │   │
│  │  │              +  Fake IoT Service Emulation                             │ │   │
│  │  │                 - Telnet (port 23)                                     │ │   │
│  │  │                 - HTTP (port 80)                                       │ │   │
│  │  │                 - SSH banner (port 22)                                 │ │   │
│  │  └─────────────────────────────────────────────────────────────────────────┘ │   │
│  │                                                                                │   │
│  │  ┌─────────────────────────────────────────────────────────────────────────┐ │   │
│  │  │                    Monitor Mode Wi-Fi Sniffer                          │ │   │
│  │  │                 - 802.11 management frames                             │ │   │
│  │  │                 - Deauthentication detection                           │ │   │
│  │  │                 - Beacon flood detection                               │ │   │
│  │  └─────────────────────────────────────────────────────────────────────────┘ │   │
│  │                                                                                │   │
│  │  ┌─────────────────────────────────────────────────────────────────────────┐ │   │
│  │  │                    Rule-Based Classifier                               │ │   │
│  │  │                 - Deauth flood (rate > threshold)                      │ │   │
│  │  │                 - Port scan (multiple ports, single source)            │ │   │
│  │  │                 - Brute force (repeated failed logins)                 │ │   │
│  │  │                 - Beacon flood (rate > threshold)                      │ │   │
│  │  └─────────────────────────────────────────────────────────────────────────┘ │   │
│  └──────────────────────────────────────────────────────────────────────────────┘   │
│                                                                                      │
│  ┌─────────────────────────────────────────────────────────────────────────────────┐ │
│  │                              OUTPUTS                                           │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌─────────────────────┐ │ │
│  │  │ OLED Display │  │  microSD     │  │  Cloud API   │  │  Local Indicators   │ │ │
│  │  │ - IP Address │  │  - Timestamp │  │  - Alerts    │  │  - Attack Count     │ │ │
│  │  │ - Attack Cnt │  │  - Payloads  │  │  - Dashboard │  │  - Status LED       │ │ │
│  │  │ - Status     │  │  - Creds     │  │  - ML Rerun  │  │                     │ │ │
│  │  └──────────────┘  └──────────────┘  └──────────────┘  └─────────────────────┘ │ │
│  └─────────────────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

### Data Flow

```
Attacker → Scans Network → Probes Decoy
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│                    ESP32-S3 Honeypot Node                    │
│  ┌─────────────────┐  ┌─────────────────┐                   │
│  │ Service Emulation│  │  Wi-Fi Sniffing│                   │
│  │ (TCP ports)     │  │  (802.11 mgmt)  │                   │
│  └────────┬────────┘  └────────┬────────┘                   │
│           │                    │                             │
│           └────────┬───────────┘                             │
│                    ▼                                         │
│           ┌─────────────────────┐                           │
│           │  Feature Extraction  │                           │
│           │ - Rate, Source, Port │                           │
│           │ - Credentials, Payload│                          │
│           └──────────┬──────────┘                           │
│                      ▼                                      │
│           ┌─────────────────────┐                           │
│           │  Rule-Based         │                           │
│           │  Classifier         │                           │
│           └──────────┬──────────┘                           │
└──────────────────────┼──────────────────────────────────────┘
                       │
                       ▼
           ┌─────────────────────┐
           │   Local Storage     │
           │   (microSD, OLED)   │
           └──────────┬──────────┘
                      │
                      ▼ (Optional Wi-Fi)
           ┌─────────────────────┐
           │  Cloud Backend      │
           │  - Aggregation      │
           │  - ML Processing    │
           │  - Dashboard        │
           └─────────────────────┘
```

---

## 🔌 Schematic & Wiring

### Pin Connections

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         ESP32-S3 Pin Mapping                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│   OLED Display (I2C)                                                     │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  VCC  ──────► 3.3V                                             │   │
│   │  GND  ──────► GND                                              │   │
│   │  SDA  ──────► GPIO8  (I2C SDA)                                │   │
│   │  SCL  ──────► GPIO9  (I2C SCL)                                │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│   microSD Module (SPI)                                                   │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  VCC  ──────► 3.3V                                             │   │
│   │  GND  ──────► GND                                              │   │
│   │  CS   ──────► GPIO10 (SPI CS)                                  │   │
│   │  MOSI ──────► GPIO11 (SPI MOSI)                                │   │
│   │  SCK  ──────► GPIO12 (SPI SCK)                                 │   │
│   │  MISO ──────► GPIO13 (SPI MISO)                                │   │
│   └─────────────────────────────────────────────────────────────────┘   │
│                                                                          │
│   Power Chain                                                            │
│   ┌─────────────────────────────────────────────────────────────────┐   │
│   │  LiPo Battery (3.7V) ──► TP4056 Charger ──► Switch ──► ESP32  │   │
│   │                        └─► 3.3V for OLED/SD                     │   │
│   └─────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────┘
```

### Wiring Diagram

```
    ┌──────────────────────────────────────────────────────────────┐
    │                                                              │
    │  ┌──────────────┐         ┌─────────────────────────────┐  │
    │  │   LiPo       │         │       TP4056 Charger        │  │
    │  │   Battery    │────────►│  ┌───────────────────┐    │  │
    │  │   3.7V       │         │  │  Type-C In        │    │  │
    │  │   1200mAh    │         │  │  Protection       │    │  │
    │  └──────────────┘         │  └─────────┬─────────┘    │  │
    │                            └────────────┼──────────────┘  │
    │                                         │                  │
    │                                    ┌────┴────┐             │
    │                                    │  SPDT   │             │
    │                                    │ Switch  │             │
    │                                    └────┬────┘             │
    │                                         │                  │
    └─────────────────────────────────────────┼──────────────────┘
                                              │
                                              ▼
    ┌──────────────────────────────────────────────────────────────┐
    │                                                              │
    │  ┌────────────────────────────────────────────────────────┐ │
    │  │                    ESP32-S3 Board                     │ │
    │  │  ┌──────────────────────────────────────────────────┐ │ │
    │  │  │  3.3V  ──────────────┬─────────────────────────┐ │ │
    │  │  │  GND   ──────────────┼─────────────────────────┘ │ │
    │  │  │  GPIO8 (SDA) ────────┼──────────────────────────┐ │ │
    │  │  │  GPIO9 (SCL) ────────┼──────────────────────────┘ │ │
    │  │  │  GPIO10 (CS) ────────┼──────────────────────────┐ │ │
    │  │  │  GPIO11 (MOSI) ──────┼──────────────────────────┘ │ │
    │  │  │  GPIO12 (SCK) ───────┼──────────────────────────┐ │ │
    │  │  │  GPIO13 (MISO) ──────┼──────────────────────────┘ │ │
    │  │  └──────────────────────────────────────────────────┘ │ │
    │  └────────────────────────────────────────────────────────┘ │
    │                                                              │
    │  ┌────────────┐              ┌────────────────────────────┐ │
    │  │   OLED     │              │       microSD Module       │ │
    │  │  ┌──────┐  │              │    ┌───────────────────┐  │ │
    │  │  │ VCC  │──┼──────────────┼────┤ VCC               │  │ │
    │  │  │ GND  │──┼──────────────┼────┤ GND               │  │ │
    │  │  │ SDA  │──┼──────────────┼────┤ CS                │  │ │
    │  │  │ SCL  │──┼──────────────┼────┤ MOSI              │  │ │
    │  │  └──────┘  │              │    │ SCK               │  │ │
    │  └────────────┘              │    │ MISO              │  │ │
    │                              │    └───────────────────┘  │ │
    │                              └────────────────────────────┘ │
    │                                                              │
    └──────────────────────────────────────────────────────────────┘
```

---

## 💻 Software Setup

### Development Environment

- **IDE**: Arduino IDE / ESP-IDF
- **Language**: C / C++
- **Libraries**:
  - `WiFi.h` - Wi-Fi management
  - `ESPAsyncWebServer.h` - HTTP emulation
  - `Adafruit_SSD1306.h` - OLED display
  - `SD.h` - microSD logging
  - `esp_wifi.h` - Monitor mode capture

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/esp32-honeypot-node.git
   cd esp32-honeypot-node
   ```

2. **Install required libraries** in Arduino IDE:
   - Adafruit SSD1306
   - Adafruit GFX Library
   - ESPAsyncWebServer
   - AsyncTCP

3. **Configure Wi-Fi credentials** in `config.h`:
   ```cpp
   #define WIFI_SSID     "your_network"
   #define WIFI_PASSWORD "your_password"
   #define AP_SSID       "HoneypotNode_AP"
   #define AP_PASSWORD   "changeme"
   ```

4. **Upload firmware**:
   - Select board: ESP32-S3 Dev Module
   - Select partition scheme: Huge APP (3MB No OTA/1MB SPIFFS)
   - Upload via USB Type-C

5. **Configure optional cloud backend**:
   - Set up ThingsBoard or Blynk
   - Update `config.h` with API endpoints

---

## 🎯 Attack Detection

### Detection Rules

| Attack Type | Feature | Threshold | Detection Rate |
|-------------|---------|-----------|----------------|
| **Deauth Flood** | Deauth frames/sec > threshold | >10/sec | 98% |
| **Beacon Flood** | Beacon frames/sec > threshold | >15/sec | 97% |
| **Port Scan** | Unique ports/sec from single source | >50/sec | 95% |
| **Brute Force** | Failed logins/sec | >5/sec | 94% |

### Detection Algorithm

```
For each frame/packet:
    Extract features:
        - Source MAC/IP
        - Frame type/subtype
        - Target port
        - Arrival time
        - Payload

    Evaluate rate-based rules:
        IF deauth_rate > THRESHOLD_DEAUTH:
            LABEL = Deauth Flood

        IF beacon_rate > THRESHOLD_BEACON:
            LABEL = Beacon Flood

        IF unique_ports > THRESHOLD_PORTS:
            LABEL = Port Scan

        IF failed_logins > THRESHOLD_BRUTE:
            LABEL = Brute Force

    Log event:
        - Timestamp
        - Source
        - Attack type
        - Metadata (credentials, payload)

    Update display:
        - Increment attack counter
        - Show latest attack

    OPTIONAL: Forward to cloud
```

### Deauthentication Detection Formula

The deauthentication detector uses a sliding window approach:

```
R_d = N_d / T

Where:
    R_d = Deauthentication frame rate
    N_d = Number of deauth frames in window
    T   = Time window duration

Alert raised when: R_d > R_th
Where R_th is calibrated from baseline traffic
```

---

## 📊 Performance Results

### Controlled Laboratory Testing

| Attack Type | Detection Accuracy | Average Accuracy |
|-------------|-------------------|------------------|
| Deauth Flood | 98% | 98% |
| Beacon Flood | 97% | 97% |
| Port Scan | 95% | 95% |
| Brute Force | 94% | 94% |

### Operational Metrics

| Metric | Value |
|--------|-------|
| Alert Latency | ~270 ms |
| Average Current Draw | ~79 mA |
| Power Saving (duty-cycled) | ~30% |
| Storage Capacity | 16GB microSD |
| Attack Log Format | Timestamped CSV |

### Performance Graph

```
Detection Accuracy by Attack Type
────────────────────────────────────────────────────────
Deauth Flood  ████████████████████████████████████▌ 98%
Beacon Flood  ███████████████████████████████████▌  97%
Port Scan     █████████████████████████████████▌    95%
Brute Force   █████████████████████████████████▌    94%
────────────────────────────────────────────────────────
              0%     50%     75%     90%    100%
```

---

## 🔄 Comparison with Alternatives

| Feature | **ESP32-S3 Honeypot** | Thinkst Canary | Raspberry Pi (T-Pot/Cowrie) |
|---------|:---------------------:|:--------------:|:---------------------------:|
| **Approximate Cost** | **~$25** | $1,000+/yr | ~$70 |
| **Power Consumption** | **Low (battery)** | Moderate (mains) | High (mains) |
| **Battery Powered** | **✅ Yes** | ❌ No | ❌ No |
| **Fake IoT Services** | **✅ Yes** | ✅ Yes | ✅ Yes |
| **Wi-Fi Deauth Capture** | **✅ Yes** | ❌ No | ⚠️ Limited |
| **Port Scan Detection** | **✅ Yes** | ✅ Yes | ✅ Yes |
| **Brute-Force Capture** | **✅ Yes** | ✅ Yes | ✅ Yes |
| **On-Device Classification** | **✅ Yes** | ✅ Yes | ⚠️ Limited |
| **Local Offline Logging** | **✅ Yes** | ❌ No | ✅ Yes |
| **Real-Time OLED Status** | **✅ Yes** | ❌ No | ❌ No |
| **Cloud Dashboard** | **✅ Yes** | ✅ Yes | ✅ Yes |
| **Vendor Support** | ❌ No | ✅ Yes | ❌ No |
| **High-Interaction Realism** | ⚠️ Limited | ✅ Yes | ✅ Yes |
| **Open-Source / Customizable** | **✅ Yes** | ❌ No | ✅ Yes |
| **Ease of Deployment** | **✅ Easy** | ✅ Easy | ⚠️ Moderate |
| **Home/Small Networks** | **✅ Yes** | ⚠️ Limited | ✅ Yes |
| **Enterprise Use** | ⚠️ Limited | ✅ Yes | ⚠️ Limited |

---

## 🚀 Quick Start

### Hardware Assembly

1. Place ESP32-S3 on MB102 breadboard
2. Connect OLED display (I2C) using jumper wires:
   - SDA → GPIO8, SCL → GPIO9, VCC → 3.3V, GND → GND
3. Connect microSD module (SPI):
   - CS → GPIO10, MOSI → GPIO11, SCK → GPIO12, MISO → GPIO13
   - VCC → 3.3V, GND → GND
4. Connect power chain:
   - LiPo → TP4056 → SPDT switch → ESP32 5V
   - ESP32 3.3V → OLED + SD module

### Software Flash

1. Open Arduino IDE
2. Install required libraries
3. Configure `config.h` with credentials
4. Select board: ESP32-S3 Dev Module
5. Compile and upload

### First Boot

1. Power on the node
2. OLED shows IP address
3. Node creates Wi-Fi AP and connects to configured network
4. Place on your network to start monitoring

---

## 🧪 Testing & Validation

### Test Environment

- **Attack Sources**: Kali Linux laptop, Raspberry Pi 4
- **Tools**: nmap, aircrack-ng/aireplay-ng, hydra
- **Network**: Isolated laboratory network
- **Duration**: Multiple test runs per attack type

### Test Commands

```bash
# Deauthentication Attack
sudo aireplay-ng -0 100 -a [BSSID] wlan0mon

# Port Scan
nmap -p- -T4 [target_IP]

# Brute Force
hydra -l admin -P passwords.txt -s 23 [target_IP] telnet

# Beacon Flood
./mdk4 wlan0mon b -c 1 -h
```

### Validation Results

```
┌─────────────────────────────────────────────────────┐
│                  ATTACK TEST RESULTS                  │
├─────────────────────────────────────────────────────┤
│ Attack Type      │ Success Rate │ Alert Latency     │
├──────────────────┼──────────────┼───────────────────┤
│ Deauth Flood     │ 98%          │ 250ms             │
│ Beacon Flood     │ 97%          │ 280ms             │
│ Port Scan        │ 95%          │ 300ms             │
│ Brute Force      │ 94%          │ 290ms             │
├──────────────────┴──────────────┴───────────────────┤
│ Benign Traffic False Alarm Rate: <2%                 │
└─────────────────────────────────────────────────────┘
```

---

## ⚠️ Challenges & Lessons Learned

| Challenge | Solution |
|-----------|----------|
| **Memory & Concurrency Limits** | N16R8 variant with 8MB PSRAM; buffer management optimization |
| **Monitor-Mode Constraints** | Custom radio driver callback interface; tuned channel hopping |
| **Threshold Calibration** | Baseline measurements; adjustable thresholds per attack |
| **Power Stability** | Wiring discipline; stable TP4056 charger module |
| **Testing Safety** | Isolated laboratory network; controlled attack generation |

---

## 🔮 Future Work

1. **🧠 On-Device ML Classification**
   - Replace rule-based classifier with compact ML model (TensorFlow Lite)
   - Train on IoT-DH honeypot dataset
   - Target: >98% accuracy with <100KB model

2. **🔧 Expanded Service Emulation**
   - Add MQTT, CoAP, and other IoT protocols
   - Increase interaction fidelity (adaptive responses)
   - Support for multiple device profiles

3. **🌐 Distributed Honeynet**
   - Coordinate multiple nodes
   - Shared dashboard and attack intelligence
   - Cross-node threat correlation

4. **⚡ Power Optimization**
   - Duty-cycled monitoring (target: 50% power reduction)
   - Deep sleep between capture periods
   - Solar charging support

5. **📈 Enhanced Analytics**
   - Integration with SIEM platforms
   - Real-time attack heatmaps
   - Automated threat reporting

---

## 📚 References

### Academic Papers

1. **[Honeypot Survey]** J. Franco et al., "A Survey of Honeypots and Honeynets for IoT, IIoT, and CPS," *IEEE Communications Surveys & Tutorials*, 2021. [arXiv:2108.02287](https://arxiv.org/abs/2108.02287)

2. **[IoT-DH Dataset]** S. Saif et al., "IoT-DH Dataset for DDoS Attack Detection," *Data in Brief*, 2024. [doi:10.1016/j.dib.2024.110496](https://doi.org/10.1016/j.dib.2024.110496)

3. **[ESP32 IDS]** A. Javed et al., "Lightweight ML-Based IDS on IoT Devices," *Future Internet*, 2024. [doi:10.3390/fi16060200](https://doi.org/10.3390/fi16060200)

4. **[ESP32 Deauth]** F. Riza et al., "Energy-Efficient ESP32 Deauthentication Detection," *Int. J. Engineering Continuity*, 2025.

5. **[HoneyIoT]** C. Guan et al., "HoneyIoT: Adaptive High-Interaction Honeypot," *WiSec '23*. [doi:10.1145/3558482.3590195](https://doi.org/10.1145/3558482.3590195)

6. **[AIIPot]** V. S. Mfogo et al., "AIIPot: Adaptive Intelligent-Interaction Honeypot," arXiv:2303.12367.

### Web Resources

- [ESP32-S3 Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3_datasheet_en.pdf)
- [Arduino ESP32 Documentation](https://docs.espressif.com/projects/arduino-esp32/en/latest/)
- [Thinkst Canary](https://canary.tools)
- [T-Pot Honeypot](https://github.com/telekom-security/tpotce)

---

## 👥 Team

| Name | ID | Contribution |
|------|----|--------------|
| **Abir Hasan Siam** | 2331218 | Hardware design, Literature Review |
| **Mohammad Kabir Hasan** | 2130390 | System Architecture, Paper Drafting |
| **Shahnaz Raihan Summy** | 2210411 | Literature Review, Detection Logic |
| **Md Eleas Biswas** | 2210099 | Software Development, Testing |

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Noor-E-Sadman** - Course Instructor, CSE216L
- **Independent University, Bangladesh** - Department of Computer Science & Engineering
- **RoboticsBD, Robotics Shop BD** - Component suppliers

---

## 📂 Project Structure

```
esp32-honeypot-node/
├── firmware/
│   ├── main/
│   │   ├── main.cpp              # Main application
│   │   ├── config.h              # Configuration
│   │   ├── wifi_manager.cpp      # Wi-Fi management
│   │   ├── service_emulation.cpp # Fake services
│   │   ├── monitor_mode.cpp      # Frame capture
│   │   ├── classifier.cpp        # Attack detection
│   │   ├── display.cpp           # OLED control
│   │   └── logger.cpp            # microSD logging
│   └── platformio.ini            # PlatformIO config
├── docs/
│   ├── images/
│   │   ├── architecture.png
│   │   ├── wiring_diagram.png
│   │   └── flow_diagram.png
│   ├── paper/
│   │   └── ESP32_Honeypot_Paper.pdf
│   └── references/
│       └── literature_review.pdf
├── tests/
│   ├── attack_generator.sh      # Test scripts
│   ├── validation.py            # Result validation
│   └── benchmark.ino            # Performance tests
├── hardware/
│   ├── schematic.pdf
│   ├── component_list.xlsx
│   └── wiring_diagram.pdf
├── web/
│   ├── dashboard/               # Cloud dashboard
│   └── api/                     # API endpoints
├── README.md
├── LICENSE
└── CONTRIBUTING.md
```

---

## 📞 Contact

- **Email**: 2331218@iub.edu.bd
- **GitHub**: [https://github.com/abir2afridi/esp32-honeypot-node](https://github.com/abir2afridi/esp32-honeypot-node)

---

<div align="center">
  <p>
    <strong>⭐ Star this repository if you find it useful!</strong><br>
    <sub>Built with ❤️ for IoT Security Research</sub>
  </p>
</div>
```
