Smart Fire Detection Abd Alert System Using IoT Technology

An Arduino-based fire detection and emergency alert system that detects flames and automatically alerts a designated phone number via SMS using a SIM900A GSM module.

The system provides **real-time fire detection, local alarms, LCD monitoring, and remote SMS notifications**.

## 🚀 Features

* 🔥 Flame detection
* 📱 Automatic SMS emergency alerts
* 🚨 Buzzer alarm
* 🔴 Red LED for fire detection
* 🟢 Green LED for normal operation
* 📟 16×2 I2C LCD status display
* 🔄 Automatic system reset after fire detection
* 🛑 Prevents repeated SMS alerts for the same fire event
* 🖥️ Serial Monitor status messages

## 🛠️ Hardware

* Arduino Uno
* Flame Sensor
* SIM900A GSM Module
* 16×2 I2C LCD
* Buzzer
* Red LED
* Green LED
* Resistors
* Jumper wires
* Breadboard
* Appropriate power supply

## 🔌 Pin Configuration

| Component    | Arduino Pin |
| ------------ | ----------- |
| Flame Sensor | D2          |
| Green LED    | D7          |
| Red LED      | D8          |
| Buzzer       | D9          |
| SIM900A      | D10, D11    |
| LCD SDA      | A4          |
| LCD SCL      | A5          |

## 📚 Libraries

The project uses the following Arduino libraries:

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <SoftwareSerial.h>
```

* `Wire` — I2C communication
* `LiquidCrystal_I2C` — LCD control
* `SoftwareSerial` — GSM communication

## ⚙️ How It Works

### Normal State

When no fire is detected:

```text
🟢 Green LED  → ON
🔴 Red LED    → OFF
🔊 Buzzer     → OFF
📟 LCD        → Monitoring... / No Fire
```

### Fire Detected

When the flame sensor detects a fire:

```text
🟢 Green LED  → OFF
🔴 Red LED    → ON
🔊 Buzzer     → ON
📟 LCD        → FIRE WARNING
📱 GSM        → Sends SMS
```

The system sends an emergency message:

```text
FIRE ALERT! Fire detected at your location!
Evacuate immediately!
```

The alarm remains active while the fire is detected.

### Fire Cleared

When the flame is no longer detected:

```text
🔴 Red LED    → OFF
🟢 Green LED  → ON
🔊 Buzzer     → OFF
📟 LCD        → Monitoring...
```

The alert state is reset, allowing the system to detect and report a new fire event.

## 🧠 Alert Control

The system uses an `alertSent` variable to prevent multiple SMS messages from being sent continuously while the same fire is present.

```cpp
bool alertSent = false;
```

Once an SMS has been sent, the system keeps the alarm active without repeatedly sending messages.

When the fire is cleared, the variable is reset.

## 📲 GSM Configuration

The SIM900A module is configured using:

```cpp
SoftwareSerial sim900a(10, 11);
```

The recipient's phone number is defined in the source code:

```cpp
const char* phoneNumber = "YOUR_PHONE_NUMBER";
```

Replace this with the intended emergency contact number before testing.

> ⚠️ Do not commit a real personal phone number to a public GitHub repository.

## ▶️ Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/USERNAME/fire-detection-system.git
```

### 2. Open the Arduino sketch

Open:

```text
fire_detection_system.ino
```

using the Arduino IDE.

### 3. Install the required libraries

Install `LiquidCrystal_I2C` if it is not already installed.

### 4. Configure the phone number

Update:

```cpp
const char* phoneNumber = "YOUR_PHONE_NUMBER";
```

### 5. Connect the hardware

Connect the components according to the pin configuration above.

### 6. Upload

Select:

```text
Board: Arduino Uno
```

Choose the correct COM/serial port and upload the program.

### 7. Monitor

Open the Arduino Serial Monitor at:

```text
9600 baud
```

## 📂 Repository Structure

```text
fire-detection-system/
│
├── README.md
├── fire_detection_system.ino
│
├── diagrams/
│   ├── circuit-diagram.png
│   ├── system-architecture.png
│   └── flowchart.png
│
└── docs/
    └── documentation.pdf
```

## 🧪 Testing

The system can be tested using the following scenarios:

| Test           | Expected Result               |
| -------------- | ----------------------------- |
| Power on       | System displays ready message |
| No flame       | Green LED ON                  |
| Flame detected | Red LED and buzzer ON         |
| Fire detected  | SMS alert sent                |
| Fire remains   | Alarm stays active            |
| Fire removed   | System resets                 |
| New fire       | New SMS alert sent            |

## 🔮 Future Improvements

* 🌫️ Add smoke detection sensors
* 🌡️ Add temperature sensors
* 📡 Add IoT/cloud connectivity
* 📱 Develop a mobile monitoring application
* 🔋 Add battery backup
* 📊 Store fire/sensor events
* 🗺️ Support multiple detection zones
* 🔔 Add multiple alarm levels
* 🔐 Improve system security and reliability

## ⚠️ Disclaimer

This project is an **educational prototype** and should not be considered a certified fire safety or life-safety system.

For real-world deployment, professional fire-safety engineering, certified sensors, reliable power systems, and appropriate regulatory testing are required.

