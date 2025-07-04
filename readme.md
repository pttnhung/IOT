# 🔥 Firefighting Robot using ESP32-CAM + Arduino Uno
-------------
This is a web-controlled firefighting robot built with an ESP32-CAM and an Arduino Uno, featuring:

🚗 Remote movement control

🎯 Servo-based camera pan/tilt

🌡 Flame sensor

💦 Water pump & buzzer alert

🌐 Web interface hosted on ESP32-CAM

🔁 UART communication from ESP32-CAM to Arduino Uno

# 📦 Features
Control robot movement (Forward, Backward, Left, Right, Stop)

Control pan/tilt angles via sliders

Set motor speed

Turn pump ON/OFF remotely

Fire detection with buzzer and automatic pump via Uno

# ⚙️ Hardware Requirements
ESP32-CAM

Arduino Uno

L298N Motor Driver

2 DC Motors

2 Servo Motors (Pan/Pan)

Flame Sensor

Relay Module

Water Pump

Buzzer

Power supply (battery or adapter)

Jumper wires, chassis, etc.

#🔌 Wiring Overview
ESP32-CAM Pinout

| Function         | GPIO   | Connected To                                         |
| ---------------- | ------ | ---------------------------------------------------- |
| TX UART          | GPIO1  | Arduino Uno RX (via logic level converter if needed) |
| Servo TILT       | GPIO15 | Tilt servo signal                                    |
| Servo PAN        | GPIO13 | Pan servo signal                                     |
| RIGHT\_MOTOR IN1 | GPIO2  | L298N IN1                                            |
| RIGHT\_MOTOR IN2 | GPIO4  | L298N IN2                                            |
| RIGHT\_MOTOR EN  | GPIO14 | L298N ENA                                            |
| LEFT\_MOTOR IN1  | GPIO0  | L298N IN3                                            |
| LEFT\_MOTOR IN2  | GPIO12 | L298N IN4                                            |
| LEFT\_MOTOR EN   | GPIO16 | L298N ENB                                            |
| GND              | GND    | Common GND                                           |

#Arduino Uno Pinout

| Pin | Function             |
| --- | -------------------- |
| D2  | Flame sensor input   |
| D3  | Buzzer output        |
| D4  | Relay (pump) control |
| D8  | RX from ESP32-CAM    |
| GND | Shared GND           |

# 🚀 How to Run the Project

1. Upload the Code
Open ESP32_CAM_Controller.ino

Use board: AI Thinker ESP32-CAM

Upload code to ESP32-CAM using USB-to-TTL adapter

Open FireSensor_Uno.ino

Use board: Arduino Uno

Upload code to Arduino Uno

2. Wire the Hardware
Wire all components as described in the tables above

Power ESP32-CAM (via 5V regulator or external supply)

Power Arduino Uno and relay system

Ensure shared GND between ESP32-CAM, L298N, Arduino

3. Use the Web Interface
Connect to Wi-Fi network created by ESP32-CAM:

SSID: Trinh Trương

Password: 123456789

Open a browser and go to: http://192.168.4.1

Use the interface to:

Move robot

Adjust Pan/Tilt

Set motor speed

Turn water pump ON/OFF

4. Fire Detection via Uno
Flame sensor connected to Arduino detects fire (LOW signal)

After 1 second delay, buzzer sounds and pump activates

ESP32-CAM can send "ON" or "OFF" to Uno via UART

"ON": immediately activate pump

"OFF": stop pump and ignore sensor for 3 seconds

📂 Robot-Firefighter-CAM
 ├── ESP32_CAM_Controller.ino   # Handles Web UI, UART, movement
 ├── FireSensor_Uno.ino         # Handles flame sensor, buzzer, relay
 ├── readme.md                  # This guide
 └── README.md                  # reports

 # ⚠️ Notes
Make sure to use a logic level converter or voltage divider if connecting ESP32-CAM TX (3.3V) to Uno RX (5V logic)

ESP32-CAM does not have USB, use a USB-to-TTL module to upload code

You may need a separate power supply for the pump/motors if high current is needed
