# 🔌 Real-Time Power Quality Monitoring System using ESP32

## 📌 Overview
This project implements a real-time power monitoring system using ESP32 microcontroller. 
It measures RMS voltage, RMS current, real power, and energy (kWh) and displays data on a 16x2 LCD.

---

## ⚙️ Features
- RMS Voltage Calculation
- RMS Current Calculation
- Real Power Calculation (V × I × PF)
- Energy Monitoring (kWh)
- LCD Display Output
- Embedded C Implementation

---

## 🧠 Working Principle
Voltage and current sensors provide analog signals to ESP32 ADC pins. 
Multiple samples are taken to calculate RMS values.

Real Power = Voltage × Current × Power Factor  
Energy = Power × Time

---

## 🔧 Hardware Used
- ESP32
- ZMPT101B Voltage Sensor
- ACS712 Current Sensor
- 16x2 LCD
- Voltage Regulator
- Capacitors
- Load Bulb

---

## 📂 Folder Structure
- software → ESP32 source code
- hardware → Circuit diagram
- docs → Project report
- images → Setup photos

---

## 📊 Applications
- Industrial Monitoring
- Residential Energy Monitoring
- Smart Grid Applications
- Energy Audit

---

## 🚀 Future Improvements
- Live Power Factor Measurement
- Data Logging
- Cloud Integration
- Fault Detection

---

## 👨‍💻 Author
Yash Bachhav
