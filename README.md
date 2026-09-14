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
vels
* 🔐 Improve system security and reliability.
