# Semi-Automatic Fire Vehicle

> **IoT Fire-Fighting Robot with ESP32 and Arduino**

A semi-automatic fire-fighting vehicle capable of detecting high temperatures and automatically activating its water-spraying system. The project combines automatic fire detection with manual remote control through a web interface.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Hardware Components](#hardware-components)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Code Structure](#code-structure)
- [Web Interface](#web-interface)
- [Troubleshooting](#troubleshooting)
- [Contributors](#contributors)
- [References](#references)

## 🎯 Overview

The **Semi-Automatic Fire-Fighting Vehicle** is a compact, IoT-enabled robot designed for fire detection and suppression. It operates in two modes:

- **Automatic Mode**: Detects flames using thermal sensors and automatically activates water pumping
- **Manual Mode**: Remote control via web interface for movement, servo control, and pump operation

## ✨ Features

### Automatic Operations
- 🔥 **Flame Detection**: Automatic fire detection using flame sensor
- 💧 **Auto Water Spray**: Automatic pump activation when fire is detected
- ⏱️ **Smart Recovery**: Resumes automatic spraying after 3 seconds if fire persists

### Manual Control
- 🕹️ **Remote Control**: Web-based interface for vehicle movement
- 🎚️ **Speed Control**: Adjustable motor speed (0-255)
- 📹 **Servo Control**: Pan (left/right) and tilt (up/down) servo movements
- 💧 **Manual Pump Control**: On/off pump control via web interface

### Connectivity
- 📶 **WiFi Access Point**: ESP32 creates its own WiFi network
- 🌐 **Web Interface**: Real-time control through web browser
- 🔄 **WebSocket Communication**: Low-latency real-time control
- 📡 **UART Communication**: ESP32-Arduino communication

## 🔧 Hardware Components

| ID | Component | Quantity | Purpose |
|----|-----------|----------|---------|
| 1 | Breadboard | 1 | Circuit connections |
| 2 | ESP32 DEV Kit V1 | 1 | Main controller & WiFi |
| 3 | BO Motor | 4 | Vehicle movement |
| 4 | Wheel | 4 | Vehicle mobility |
| 5 | L298N Motor Driver | 1 | Motor control |
| 6 | Flame Sensor | 1 | Fire detection |
| 7 | Servo SG90 | 2 | Pan/tilt mechanism |
| 8 | Water Pump (5-9V) | 1 | Water spraying |
| 9 | Water Bottle | 1 | Water reservoir |
| 10 | Battery | 3 | Power supply |
| 11 | RELAY SRD-05VDC-SL-C | 1 | Pump control |
| 12 | DC-DC Converter | 1 | Voltage regulation |
| 13 | Arduino Uno | 1 | Flame sensor processing |

## 🏗️ System Architecture

```
┌─────────────────┐    WiFi     ┌─────────────────┐
│   Web Browser   │◄──────────►│     ESP32       │
│  (User Control) │             │  (Main Control) │
└─────────────────┘             └─────────────────┘
                                         │
                                      UART
                                         │
                                         ▼
                                ┌─────────────────┐
                                │   Arduino Uno   │
                                │ (Flame Sensor)  │
                                └─────────────────┘
```

### Communication Flow
1. **Web Interface** ↔ **ESP32** (WebSocket/HTTP)
2. **ESP32** ↔ **Arduino** (UART Serial)
3. **ESP32** → **Motors/Servos/Pump** (PWM/Digital)
4. **Arduino** → **Flame Sensor** (Analog/Digital)

## 🚀 Installation

### Prerequisites
- Arduino IDE with ESP32 board support
- Required libraries (see below)

### Required Libraries
Install these libraries through Arduino Library Manager:

```bash
# ESP32 Libraries
- ESP32Servo
- AsyncTCP
- ESPAsyncWebServer

# Standard Libraries (usually pre-installed)
- WiFi
- iostream
- sstream
```

### Hardware Setup
1. **Power Connections**: Connect batteries and DC-DC converter
2. **Motor Wiring**: Connect BO motors to L298N driver
3. **Sensor Setup**: Connect flame sensor to Arduino
4. **Servo Mounting**: Attach servos for pan/tilt mechanism
5. **Pump Installation**: Connect water pump through relay
6. **Communication**: Wire UART between ESP32 and Arduino

### Software Installation
1. Clone or download the project files
2. Open `esp32_fire_vehicle.ino` in Arduino IDE
3. Select **ESP32 Dev Module** as board
4. Configure WiFi credentials in the code:
   ```cpp
   const char *ssid = "Your_Network_Name";
   const char *password = "Your_Password";
   ```
5. Upload the code to ESP32

## 📱 Usage

### Initial Setup
1. Power on the vehicle
2. ESP32 creates WiFi Access Point: `"Trinh Trương"`
3. Connect your device to this network (Password: `123456789`)
4. Open web browser and navigate to: `192.168.4.1`

### Web Interface Controls

#### Movement Controls
- **⬆️ Forward**: Move vehicle forward
- **⬇️ Backward**: Move vehicle backward  
- **⬅️ Left**: Turn vehicle left
- **➡️ Right**: Turn vehicle right

#### Adjustment Controls
- **Speed Slider**: Adjust motor speed (0-255)
- **Tilt Slider**: Control vertical servo angle (0-180°)
- **Pan Slider**: Control horizontal servo angle (0-180°)

#### Pump Controls
- **PUMP ON**: Manually activate water pump
- **PUMP OFF**: Manually deactivate water pump

### Automatic Mode
- Vehicle automatically detects flames
- Pump activates automatically when fire is detected
- If manually turned off, auto-mode resumes after 3 seconds

## 📁 Code Structure

```
esp32_fire_vehicle.ino
├── Headers & Definitions
├── Hardware Configuration
│   ├── Motor pin definitions
│   ├── Servo pin definitions
│   └── Communication settings
├── Web Interface (HTML/CSS/JS)
├── Motor Control Functions
│   ├── rotateMotor()
│   ├── moveCar()
│   └── setUpPinModes()
├── Web Server Handlers
│   ├── handleRoot()
│   ├── handleNotFound()
│   └── WebSocket events
├── Setup Function
│   ├── Serial initialization
│   ├── WiFi AP setup
│   ├── Web server configuration
│   └── Hardware initialization
└── Main Loop
    └── WebSocket cleanup
```

### Key Functions

- **`moveCar(int inputValue)`**: Controls vehicle movement
- **`rotateMotor(int motorNumber, int motorDirection)`**: Individual motor control
- **`onCarInputWebSocketEvent()`**: Handles real-time web commands
- **`setUpPinModes()`**: Initializes all hardware pins

## 🌐 Web Interface

The web interface provides a responsive control panel with:

### Visual Elements
- **Directional Arrows**: Large, touch-friendly movement buttons
- **Sliders**: Real-time adjustment controls
- **Pump Buttons**: Clear ON/OFF controls with status feedback
- **Mobile Responsive**: Works on phones, tablets, and computers

### Technical Features
- **WebSocket Connection**: Real-time, low-latency control
- **Auto-Reconnection**: Automatically reconnects if connection drops
- **Touch Support**: Works with both mouse and touch inputs
- **Visual Feedback**: Button press animations and status updates

## 🔧 Troubleshooting

### Common Issues

**WiFi Connection Problems**
- Ensure ESP32 is powered and running
- Check if "Trinh Trương" network appears in WiFi list
- Verify password: `123456789`

**Vehicle Not Moving**
- Check battery levels
- Verify motor connections to L298N
- Ensure PWM channels are properly configured

**Pump Not Working**
- Check relay connections
- Verify pump power supply (5-9V)
- Test manual pump controls first

**Web Interface Not Loading**
- Try accessing `192.168.4.1` directly
- Clear browser cache
- Check if multiple devices are connected (may cause conflicts)

### Debug Mode
Enable debug output by monitoring Serial console at 115200 baud rate.

## 👥 Contributors

**University of Danang - VNUK Institute**  
**Course**: CSB43058 - Internet of Things  
**Lecturer**: Mr. Dam Minh Tung

### Team Members
- **Phan Thi Thuy Nhung** - 23020006 (Computer Science & Engineering K23)
- **Tran Bao Nhi** - 22090015 (Software Engineering K22)  
- **Truong Tuyet Trinh** - 22090005 (Software Engineering K22)

**Academic Year**: 2024-2025

## 📚 References

### Video Tutorials
- [Fire Fighting Robot Tutorial](https://www.youtube.com/watch?v=jsvAL9ogFBw&t=17s&ab_channel=SaadInnovativeIdeas)
- [Arduino Motor Control](https://www.youtube.com/watch?v=-2QauRxO-iA&ab_channel=NShop-Linhki%E1%BB%87n%C4%90i%E1%BB%87nt%E1%BB%AD)
- [ESP32 Web Server](https://www.youtube.com/watch?v=OBU7RXKxkr0&t=920s)

### Documentation
- [Arduino Official Documentation](https://www.arduino.cc/)
- [Arduino Vietnam Community](http://arduino.vn/)

---

## 🚨 Safety Notes

- Always supervise the vehicle during operation
- Ensure water reservoir is properly secured
- Keep electrical components away from water
- Use appropriate power ratings for all components
- Test in safe environment before real fire scenarios

## 📄 License

This project is created for educational purposes as part of IoT coursework at VNUK Institute, University of Danang.

---

**For technical support or questions, please contact the development team.**# IOT
