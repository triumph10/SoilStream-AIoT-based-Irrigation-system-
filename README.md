# SoilStream  
### Smart Solar-Powered AIoT System for Real-Time Soil Moisture Monitoring and Automated Irrigation

<div align="center">

![IoT](https://img.shields.io/badge/IoT-Smart%20Agriculture-green)
![AI](https://img.shields.io/badge/AI-Powered-blue)
![ML](https://img.shields.io/badge/Machine%20Learning-orange)
![Firebase](https://img.shields.io/badge/Firebase-Backend-yellow)
![React Native](https://img.shields.io/badge/React%20Native-Mobile%20App-61DAFB)
![ESP32](https://img.shields.io/badge/ESP32-Microcontroller-red)

</div>

---

## Overview

**SoilStream** is a smart solar-powered AIoT (Artificial Intelligence of Things) agricultural system designed to modernize irrigation and crop management using real-time monitoring, machine learning, and intelligent automation.

The platform integrates:

- IoT-based environmental sensing
- Smart automated irrigation
- Rainfall prediction
- AI-based crop identification
- Pest & disease diagnosis
- Cloud-based analytics
- Solar-powered hardware infrastructure

The system continuously monitors soil moisture, temperature, humidity, and atmospheric pressure to automate irrigation and improve agricultural efficiency while reducing water wastage.

---

# Features

## Real-Time Soil Monitoring
- Live soil moisture tracking
- Temperature & humidity monitoring
- Atmospheric pressure sensing
- Real-time cloud synchronization

## Smart Automated Irrigation
- AI-driven irrigation decisions
- Automatic pump control
- Water conservation optimization
- Crop-specific watering logic

## Rainfall Prediction
- Machine learning-based weather prediction
- Intelligent irrigation scheduling
- Prevents unnecessary watering

## AI Crop Identification
- Upload crop images
- AI-powered crop recognition
- Crop-specific recommendations

## Pest & Disease Detection
- Plant disease diagnosis using AI
- Pest identification from leaf images
- Automated remedy suggestions

## Mobile Application
- Real-time monitoring dashboard
- Manual pump override
- Crop analysis interface
- Smart irrigation controls

---

# System Architecture

## Hardware Components
- ESP32-WROOM-32
- Capacitive Soil Moisture Sensor
- BME280 Sensor
- Relay Module
- Water Pump
- Solar Panel
- Li-ion Battery
- TP4056 Charging Module

## Software Stack

### Frontend
- React Native
- Expo
- JavaScript

### Backend
- Flask
- Node.js
- Firebase Cloud Functions

### Database
- Firebase Firestore

### Machine Learning
- TensorFlow
- CNN Models
- LightGBM
- Python

---

# Working Flow

1. IoT sensors collect real-time environmental data.
2. Data is transmitted to Firebase Cloud.
3. Machine learning models analyze weather and soil conditions.
4. Smart irrigation decisions are generated automatically.
5. Water pump is controlled using relay-based automation.
6. Farmers receive real-time insights via the mobile app.

---

# AI Modules

## Rainfall Prediction Engine
The ML model predicts rainfall probability using:
- Temperature
- Humidity
- Pressure
- Seasonal patterns

## Crop Identification
CNN-based image classification model for:
- Crop recognition
- Crop-specific recommendations

## Pest & Disease Diagnosis
AI-powered image analysis system for:
- Disease detection
- Pest identification
- Treatment recommendations

---

# Smart Irrigation Logic

```text
IF Rain Expected
    → Pump OFF

ELSE IF Soil Dry
    → Pump ON

ELSE IF Soil Wet
    → Pump OFF

ELSE
    → Maintain Current State
```

---

# Project Structure

```bash
SoilStream/
│
├── hardware/
│   ├── esp32_code/
│   ├── sensor_modules/
│   └── relay_control/
│
├── backend/
│   ├── flask_server/
│   ├── firebase_functions/
│   └── ai_models/
│
├── mobile_app/
│   ├── screens/
│   ├── components/
│   └── services/
│
├── datasets/
├── documentation/
└── README.md
```

---

# Installation

## Clone Repository

```bash
git clone https://github.com/your-username/SoilStream.git
```

## Install Frontend Dependencies

```bash
cd mobile_app
npm install
```

## Start Mobile Application

```bash
npx expo start
```

## Install Backend Dependencies

```bash
cd backend
pip install -r requirements.txt
```

## Run Flask Backend

```bash
python app.py
```

---

# Key Benefits

- Precision agriculture
- Reduced water wastage
- Sustainable farming
- AI-driven crop management
- Real-time monitoring
- Automated irrigation
- Renewable energy integration

---

# Future Scope

- Soil nutrient analysis
- pH monitoring
- Fertilizer recommendation engine
- Edge AI deployment
- Multi-farm scalability
- Drone integration

---

# Authors

- Siddesh Patil
- Raj Choudhary
- Varun Lad
- Devesh Patil

Department of Computer Science & Engineering (Data Science)  
A.P. Shah Institute of Technology  
University of Mumbai

---

# License

This project is developed for academic and research purposes.

---

# Acknowledgement

We sincerely thank our project guides, faculty members, and the Department of Computer Science & Engineering (Data Science), A.P. Shah Institute of Technology, for their valuable guidance and support throughout the development of this project.