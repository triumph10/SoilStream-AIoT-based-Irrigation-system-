<div align="center">

# SoilStream

### Solar-Powered AIoT System for Real-Time Soil Monitoring and Automated Irrigation

[![IEEE CONIT 2026](https://img.shields.io/badge/IEEE_CONIT_2026-Accepted-blue?style=flat-square&logo=ieee)](https://d2tna6wv3bmh8.cloudfront.net/research_paper.pdf)
[![Patent](https://img.shields.io/badge/Patent-202621042187-green?style=flat-square)](https://d2tna6wv3bmh8.cloudfront.net)
[![Copyright](https://img.shields.io/badge/Copyright-SW--13522%2F2026--CO-orange?style=flat-square)](https://d2tna6wv3bmh8.cloudfront.net)
[![ESP32](https://img.shields.io/badge/ESP32-Firmware-red?style=flat-square)](hardware/)
[![React Native](https://img.shields.io/badge/React_Native-Mobile-61DAFB?style=flat-square&logo=react)](mobile_app/)
[![Firebase](https://img.shields.io/badge/Firebase-Backend-FFCA28?style=flat-square&logo=firebase)](backend/)

**[📄 Research Paper](https://d2tna6wv3bmh8.cloudfront.net/research_paper.pdf) · [📋 Project Report](https://d2tna6wv3bmh8.cloudfront.net/project_report.pdf) · [🖼️ Poster](https://d2tna6wv3bmh8.cloudfront.net/poster.pdf) · [💻 Source Code](https://github.com/RajChoudhary99/SoilStream)**

</div>

---

## 🌐 Read the Full Write-Up

> **[Building a Solar-Powered Smart Irrigation System That Actually Thinks](https://d2tna6wv3bmh8.cloudfront.net)**

The blog covers the full story — why existing IoT irrigation systems fail in monsoon-dependent regions, how each layer of SoilStream (hardware, ML models, decision engine, mobile app) was designed and why, what broke during development (EfficientNetB0's training collapse, building a Konkan-specific rainfall dataset from scratch), and the complete results with model comparisons.

If you're trying to understand the project or build something similar, start there.

---

SoilStream is a closed-loop AIoT platform that monitors real-time soil and atmospheric conditions, predicts rainfall using machine learning, identifies crop type from images, and automates irrigation — powered entirely by solar energy.

---

## Architecture

```
┌─────────────────────────────────────────────────┐
│                  FIELD HARDWARE                 │
│   ESP32 ← BME280 + Soil Sensor → Solar Panel   │
│                Relay → Water Pump               │
└───────────────────────┬─────────────────────────┘
                        │ MQTT / HTTPS
┌───────────────────────▼─────────────────────────┐
│              FIREBASE CLOUD BACKEND             │
│       Realtime DB · Cloud Functions · Flask     │
└──────────┬──────────────────┬───────────────────┘
           │                  │
  ┌────────▼───────┐  ┌───────▼────────┐
  │ Rainfall Model │  │  Crop ID Model │
  │  SVR · 92.86%  │  │ ResNet50 · 99.7│
  └────────┬───────┘  └───────┬────────┘
           └─────────┬─────────┘
              ┌──────▼──────────────┐
              │   DECISION ENGINE   │
              │  Rain? → Pump OFF   │
              │  Wet?  → Pump OFF   │
              │  Else  → Pump ON    │
              └──────┬──────────────┘
                     │
          ┌──────────▼──────────────┐
          │   REACT NATIVE APP      │
          │  Dashboard · Overrides  │
          └─────────────────────────┘
```

---

## ML Results

### Crop Identification

| Model | Test Accuracy | F1 Score |
|---|---|---|
| **ResNet50** | **99.7%** | **0.97** |
| VGG16 | 95.6% | 0.95 |
| EfficientNetB0 | 16.0%* | 0.07 |

*\*Training collapse detected — rejected despite high validation accuracy.*

### Rainfall Prediction (Konkan Region Dataset)

| Model | Accuracy | Precision | F1 |
|---|---|---|---|
| **SVR** | **92.86%** | **0.9257** | **0.9103** |
| LightGBM | 92.32% | 0.9087 | 0.9047 |
| GRU | 92.30% | 0.9195 | 0.9031 |

> SVR was selected by prioritising **precision over recall** — a false positive (predicting rain that doesn't come) leaves crops dry; the costlier failure in a monsoon-dependent region.

---



## License

Developed for academic and research purposes.  
Patent filed — IP India, Application No. `202621042187`.  
Software registered — Copyright Office, GoI, `SW-13522/2026-CO`.  
Unauthorised commercial use is prohibited.