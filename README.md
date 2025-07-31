# 🤖 Industrial Intelligent Line Follower Robot

This repository contains the code, documentation, and circuit design for an **intelligent industrial-grade line following robot**. Designed for warehouse automation and material handling applications, the robot uses IR sensors and PID control for high-precision line tracking.

---

## 🚀 Features

- Smooth and stable line tracking using PID control
- Modular code structure with tunable PID parameters
- IR sensor array for line position detection
- Works on curves, junctions, and high-speed paths
- L298N motor driver support
- Easily scalable for industrial paths

---

## 🧠 Working Principle

1. Five IR sensors detect the black line on a white surface.
2. The Arduino calculates the robot’s position relative to the center of the line.
3. A PID algorithm adjusts the speed of both motors to correct direction.
4. The robot maintains its path precisely, even at turns.

---

## 🛠️ Hardware Required

- Arduino UNO
- IR Sensor Array (5 sensors)
- L298N Motor Driver
- 2 DC Motors + Wheels
- Power Supply (7.4V Li-ion or 9V)
- Jumper wires, chassis

---

## 📐 Circuit Diagram

<img width="1314" height="713" alt="Image" src="https://github.com/user-attachments/assets/c98e3a4f-e325-4d8d-a58e-e30bfadc9d3d" />

## 💻 Code Overview

Located in 


