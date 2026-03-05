# Software Setup Guide

The SkyMapper software stack handles real-time data collection, autonomous flight control, and web-based 3D reconstruction. It operates on a highly efficient closed-loop architecture.

## 🏗️ Software Architecture Overview
The system consists of three main operational nodes communicating in real-time:
1. **Mobile Node (Smartphone):** Executes VIO tracking and captures targeted images.
2. **Control Node (Flight Controller):** Processes autonomous view planning and sends waypoints to the UAV.
3. **Server Node (Web Server):** Archives incoming data and processes the final 3D reconstruction.

## 💻 1. Web Server & Data Archiving
A central web server acts as the primary data hub for the entire system, enabling targeted remote monitoring.
- **Function:** Receives 6DoF pose data and high-resolution images from the smartphone via a wireless network.
- **Reconstruction Pipeline:** Archives data to enable diverse downstream applications, ultimately generating highly accurate (7-12cm error) 3D spatial models.
- **Setup:** The provided server scripts can be deployed on a local workstation or a cloud-based instance (e.g., AWS, GCP).

## 📱 2. Mobile Application (Sensor Node)
A custom application runs on the mounted smartphone to handle environmental perception.
- **Initialization:** Starts the Vision-Inertial Odometry (VIO) pipeline to establish a global coordinate system.
- **Data Capture:** Triggers the camera shutter automatically based on spatial distance intervals to ensure optimal overlap for photogrammetry (72-99% coverage).
- **Streaming:** Streams telemetry and image data to the Web Server continuously.

## ✈️ 3. Autonomous Flight Controller
The closed-loop control system enables the drone to navigate and scan unknown indoor environments safely.
- **Path Planning:** The algorithm calculates the next best view dynamically, ensuring thorough scanning of the targeted remote area.
- **Execution:** Uses the drone manufacturer's SDK to translate the planned paths into precise movement commands, guided by the smartphone's real-time trajectory estimation.