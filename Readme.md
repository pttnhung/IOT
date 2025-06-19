🔥 Firefighting Robot using ESP32 + Arduino Uno

If you have ESP32 devkit V1: just copy all code in main branch 

This project is a remote-controlled firefighting robot using ESP32 DevKit V1 and Arduino Uno, featuring:

Motor control (L298N)

Pan/Tilt servo camera control

Fire detection with buzzer & pump

Web interface (via Wi-Fi)

Communication between ESP32 ↔ Uno via UART

📦 Features
🚗 Control movement (forward, backward, left, right, stop)

🎯 Pan/Tilt camera via sliders

🌡 Fire sensor (flame detection)

🔔 Buzzer alarm and water pump relay

📱 Mobile-friendly Web UI (HTML/JS)

🧠 ESP32 handles logic + sends UART commands to Uno

⚙️ Hardware Requirements
ESP32 DevKit V1

Arduino Uno

Flame Sensor

Buzzer

Relay Module + Water Pump

L298N Motor Driver

2 DC Motors

2 Servo Motors (for pan/tilt)

Jumper wires, power supply, chassis

🔌 Wiring Overview
ESP32 DevKit V1

| Function        | GPIO   | Connect To          |
| --------------- | ------ | ------------------- |
| UART TX2        | GPIO17 | Arduino Uno RX (D8) |
| Servo PAN       | GPIO13 | Servo signal        |
| Servo TILT      | GPIO15 | Servo signal        |
| Motor Left IN1  | GPIO27 | L298N IN1           |
| Motor Left IN2  | GPIO26 | L298N IN2           |
| Motor Right IN3 | GPIO25 | L298N IN3           |
| Motor Right IN4 | GPIO33 | L298N IN4           |
| PWM Left (ENA)  | GPIO14 | L298N ENA           |
| PWM Right (ENB) | GPIO32 | L298N ENB           |
| GND             | GND    | Common GND          |
| 5V (optional)   | 5V     | L298N VCC           |

Arduino Uno

| Pin | Function      |
| --- | ------------- |
| D2  | Flame sensor  |
| D3  | Buzzer        |
| D4  | Relay module  |
| D8  | RX from ESP32 |
| GND | Common GND    |

🚀 How to Run
1. Flash Code
Open ESP32_Controller.ino in Arduino IDE

Select board: ESP32 Dev Module

Upload to ESP32 DevKit V1

Open FireSensor_Uno.ino in Arduino IDE

Select board: Arduino Uno

Upload to Arduino Uno

2. Power & Connect Hardware
Connect all wires based on the table above

Power ESP32 and Arduino (via USB or battery)

Make sure GND is shared across all modules

3. Access the Web Control Panel
From your phone/laptop, connect to Wi-Fi:

SSID: Trinh Trương

Password: 123456789

-----
// You can edit SSID and Password in ESP32 code 
const char *ssid = "Trinh Trương";
const char *password = "123456789";
-----

Open a browser and go to: http://192.168.4.1

Use the interface to:

Move robot

Pan/tilt camera

Turn pump ON/OFF

4. Fire Detection Logic
Arduino detects fire via flame sensor (LOW signal)

It activates buzzer and water pump after 1 second

If ESP32 sends "OFF", Uno disables pump and ignores fire for 3 seconds

If ESP32 sends "ON", Uno immediately activates pump manually

📂 Robot-Firefighter
 ├── ESP32_vehicle.ino      # Web UI + motor + UART
 ├── Arduino_Uno.ino        # Flame detection + buzzer + relay
 ├── readme.md              # This guide
 └── README.md              # reports
