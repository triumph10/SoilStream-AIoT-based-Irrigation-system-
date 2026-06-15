<div align="center">

<img src="https://img.shields.io/badge/IEEE_CONIT_2026-Accepted-blue?style=for-the-badge&logo=ieee" />
<img src="https://img.shields.io/badge/Patent-202621042187-green?style=for-the-badge" />
<img src="https://img.shields.io/badge/Copyright-SW--13522%2F2026--CO-orange?style=for-the-badge" />

# SoilStream

### A Solar-Powered AIoT System for Intelligent Soil Monitoring and Automated Irrigation

*Accepted at IEEE 6th International Conference on Intelligent Technologies (CONIT 2026)*

[📄 Paper](https://d2tna6wv3bmh8.cloudfront.net/research_paper.pdf) · [📋 Project Report](https://d2tna6wv3bmh8.cloudfront.net/project_report.pdf) · [🖼️ Poster](https://d2tna6wv3bmh8.cloudfront.net/poster.pdf) · [🌐 Blog](https://d2tna6wv3bmh8.cloudfront.net)

</div>

---

## Overview

Farmers in India's Konkan region lose water, money, and crops to a solvable problem — irrigation systems that can't tell if rain is two hours away. The pump runs, the monsoon arrives, and water is wasted at scale.

**SoilStream** is a closed-loop AIoT platform that monitors soil and atmospheric conditions in real time, predicts local rainfall using machine learning, identifies crop type from leaf images, and only irrigates when it genuinely makes sense — all powered by solar energy with no dependency on the grid.

---

## Research & IP

| | |
|---|---|
| **Conference** | IEEE CONIT 2026 · KLE Institute of Technology, Hubballi · Paper ID: 960 |
| **Patent** | Intellectual Property India, GoI · Application No: `202621042187` |
| **Copyright** | Copyright Office, GoI · Registration No: `SW-13522/2026-CO` |

---

## Key Results

### Crop Identification (CNN Comparison)

| Model | Test Accuracy | Val. Accuracy | Weighted F1 | Status |
|---|---|---|---|---|
| **ResNet50** | **99.7%** | 96.48% | **0.97** | ✅ Selected |
| VGG16 | 95.6% | 94.04% | 0.95 | Fallback |
| EfficientNetB0 | 16.0%* | 99.76% | 0.07 | ❌ Rejected |

*\*Training collapse detected despite high validation accuracy — ruled out at inference.*

### Rainfall Prediction (Coastal Dataset — Konkan Region)

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| **SVR** | **92.86%** | **0.9257** | 0.8954 | **0.9103** |
| LightGBM | 92.32% | 0.9087 | 0.9007 | 0.9047 |
| GRU | 92.30% | 0.9195 | 0.8873 | 0.9031 |

> **Why SVR?** Precision was prioritised over raw accuracy. A false positive (predicting rain when there's none) keeps the pump off when it shouldn't be — the costlier error in a monsoon-dependent region.

### Rainfall Prediction (Extended Region Dataset)

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| SVR | 91.47% | **0.9310** | 0.8725 | 0.9008 |
| LightGBM | **91.55%** | 0.9232 | 0.8832 | 0.9027 |
| GRU | 91.38% | 0.9166 | 0.8863 | 0.9012 |

---

## System Architecture

SoilStream is composed of four layers working in a continuous closed loop:

```
┌─────────────────────────────────────────────────────────────┐
│                        FIELD HARDWARE                       │
│   ESP32 ← BME280 + Soil Sensor → Solar Panel + Battery     │
│                Relay → Submersible Pump                     │
└────────────────────────┬────────────────────────────────────┘
                         │ MQTT / HTTPS
┌────────────────────────▼────────────────────────────────────┐
│                      CLOUD BACKEND                          │
│        Firebase Realtime DB + Cloud Functions + Flask       │
└─────────┬─────────────────────┬───────────────┬────────────┘
          │                     │               │
┌─────────▼──────┐   ┌──────────▼──────┐  ┌────▼──────────────┐
│ Rainfall Model │   │  Crop ID Model  │  │  Pest Detection   │
│  SVR · 92.86%  │   │ ResNet50 · 99.7%│  │  (Kindwise API)   │
└─────────┬──────┘   └──────────┬──────┘  └────┬──────────────┘
          └──────────────────────┴───────────────┘
                                 │
                    ┌────────────▼───────────────┐
                    │    DECISION ENGINE          │
                    │  Pump ON only when:         │
                    │  • Soil below threshold AND  │
                    │  • Rain probability < 60%   │
                    │  • No disease detected      │
                    └────────────┬───────────────┘
                                 │
                    ┌────────────▼───────────────┐
                    │    REACT NATIVE MOBILE APP  │
                    │  Live dashboard · Overrides │
                    │  Crop ID · Disease scan     │
                    └────────────────────────────┘
```

---

## Hardware Components

| Component | Role |
|---|---|
| ESP32-WROOM-32 | Core microcontroller |
| BME280 | Temperature, humidity, atmospheric pressure |
| Capacitive Soil Moisture Sensor | Real-time soil saturation |
| Relay Module (5V) | Pump control |
| Submersible Water Pump | Irrigation actuation |
| 6V Solar Panel + TP4056 | Renewable power input & charging |
| 18650 Li-ion Battery | Off-sun power storage |

---

## Tech Stack

**Firmware**
- ESP32 (Arduino / C++)

**ML & Backend**
- Python · Flask
- TensorFlow / Keras (ResNet50, VGG16, EfficientNetB0)
- SVR · LightGBM · GRU
- Firebase Cloud Functions · Node.js

**Data Sources**
- Meteostat (historical atmospheric data)
- Indian Meteorological Department (IMD) rainfall records

**APIs**
- Kindwise API (pest & disease diagnosis)
- Gemini API

**Mobile**
- React Native · Expo · JavaScript

**Database & Cloud**
- Firebase Realtime Database · Firestore

---

## Project Structure

```
SoilStream/
│
├── hardware/
│   ├── esp32_code/          # Sensor reading, relay control, MQTT publish
│   ├── sensor_modules/      # BME280 & soil sensor drivers
│   └── relay_control/       # Pump actuation logic
│
├── backend/
│   ├── flask_server/        # REST API for ML inference
│   ├── firebase_functions/  # Cloud triggers & automation
│   └── ai_models/           # Trained .h5 / .pkl model files + notebooks
│
├── mobile_app/
│   ├── screens/             # Dashboard, crop ID, disease scan
│   ├── components/          # Reusable UI components
│   └── services/            # Firebase sync, API clients
│
├── datasets/                # Meteostat + IMD processed datasets
├── documentation/           # Report, paper, poster PDFs
└── README.md
```

---

## Getting Started

### Prerequisites
- Node.js ≥ 18
- Python ≥ 3.9
- Expo CLI
- Firebase project with Realtime Database enabled
- Arduino IDE (for ESP32 flashing)

### Clone

```bash
git clone https://github.com/RajChoudhary99/SoilStream.git
cd SoilStream
```

### Mobile App

```bash
cd mobile_app
npm install
npx expo start
```

### Backend (Flask)

```bash
cd backend
pip install -r requirements.txt
python app.py
```

### ESP32 Firmware

Open `hardware/esp32_code/main.ino` in Arduino IDE, configure your WiFi credentials and Firebase URL in `config.h`, then flash to your ESP32.

---

## How the Irrigation Decision Works

```
IF  rain probability ≥ 60%         → Pump OFF  (rain is coming)
ELSE IF  soil moisture ≥ threshold  → Pump OFF  (soil is wet enough)
ELSE IF  disease detected           → Pump OFF  (flag for review)
ELSE                                → Pump ON
```

The conservative logic avoids waterlogging during unpredictable monsoon seasons without over-relying on any single data source.

---

## Future Scope

- Soil nutrient (NPK) and pH monitoring
- AI-driven fertilizer recommendation
- Edge AI deployment (TensorFlow Lite on ESP32-S3)
- Multi-farm dashboard with geospatial mapping
- Drone integration for aerial crop scouting

---

## Authors

**Raj Choudhary · Siddesh Patil · Varun Lad · Devesh Patil**

Department of Computer Science & Engineering (Data Science)
A.P. Shah Institute of Technology, University of Mumbai

---

## License

This project is developed for academic and research purposes.
Patent filed with Intellectual Property India (Application No. 202621042187).
Software registered with the Copyright Office, Government of India (SW-13522/2026-CO).

Unauthorised commercial use is prohibited.

---

<div align="center">

*If this project helped you, consider starring the repository.*

</div>