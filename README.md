🌱 Home Soil Moisture Detection System

An Arduino-based Soil Moisture Detection System designed to monitor the moisture condition of soil for home gardening and plant-care applications.

The system uses a soil moisture sensor to detect changes in soil moisture and sends the sensor signal to an Arduino Uno. Arduino processes the reading and provides an output indication through an LED or other output device.

«🌿 Healthy Plants, Happier Homes»

---

📌 Overview

Plants need an appropriate amount of water for healthy growth. Both insufficient watering and excessive watering can affect plant health.

This project demonstrates a simple electronics-based solution for monitoring soil moisture at home.

The basic system consists of:

Soil → Soil Moisture Sensor → Arduino Uno → Processing → LED/Output

The project is useful for learning Arduino programming, sensor interfacing, basic electronics, and microcontroller-based automation.

---

✨ Features

- 🌱 Detects soil moisture conditions
- 🔌 Arduino-based control system
- 💧 Uses a soil moisture sensor
- 💡 Provides visual output using an LED
- 📊 Supports analog sensor readings
- 🪴 Suitable for home gardening
- 🔧 Simple and low-cost prototype
- 🚀 Can be expanded into an automatic irrigation system
- 📡 Can be upgraded with IoT and Wi-Fi connectivity

---

🧰 Components Required

No.| Component| Purpose
1| Arduino Uno| Main microcontroller
2| Soil Moisture Sensor| Detects soil moisture condition
3| Breadboard| Makes circuit connections
4| Jumper Wires| Connects the components
5| LED| Indicates the detected condition
6| 220Ω Resistor| Limits LED current
7| USB Cable| Programming and power
8| Plant Pot & Soil| Testing environment

Optional Components for Future Expansion

- Relay module
- DC water pump
- ESP32/ESP8266
- LCD/OLED display
- Wi-Fi connection
- Mobile application
- Cloud data logging

---

🔌 Circuit Connections

For a common soil moisture sensor module with VCC, GND, AO and DO pins, the basic analog connection can be made as follows:

Soil Moisture Sensor| Arduino Uno
VCC| 5V
GND| GND
AO| A0
DO| Not required for analog reading

LED Connection

LED| Arduino
LED positive/anode| Digital Pin 7
LED negative/cathode| 220Ω resistor → GND

Basic Circuit

        SOIL
          │
          ▼
 ┌──────────────────┐
 │ Soil Moisture    │
 │     Sensor       │
 └────────┬─────────┘
          │
          │ AO
          ▼
      ┌─────────┐
      │ Arduino │
      │   Uno   │
      └────┬────┘
           │
           │ D7
           ▼
        ┌─────┐
        │ LED │
        └──┬──┘
           │
        220Ω
           │
          GND

«Note: Sensor readings and the dry/wet threshold depend on the particular sensor and soil. The threshold should be calibrated rather than assuming one universal value.»

---

⚙️ Working Principle

The soil moisture sensor is inserted into the soil near the plant.

The sensor detects changes associated with the moisture condition of the soil and generates an electrical output.

The Arduino receives the sensor output through an analog input.

The Arduino program then:

1. Reads the sensor value.
2. Processes the reading.
3. Compares it with a selected threshold.
4. Determines the soil condition.
5. Controls the LED/output accordingly.

Working Flow

🌱 Soil
   ↓
💧 Soil Moisture Sensor
   ↓
🔌 Arduino Uno
   ↓
📊 Analog Sensor Reading
   ↓
⚙️ Program/Threshold
   ↓
💡 LED / Output

---

🔄 Step-by-Step Operation

Step 1 — Power the System

Connect the Arduino Uno to a computer using a USB cable.

Step 2 — Connect the Sensor

Connect the sensor's VCC, GND and analog output to the Arduino.

Step 3 — Place the Sensor

Insert the moisture sensor into the soil of the plant pot.

Step 4 — Detect Moisture

The sensor detects changes in the soil condition.

Step 5 — Read the Sensor

Arduino reads the sensor using its analog input.

Step 6 — Process the Reading

The program compares the sensor reading with a selected threshold.

Step 7 — Display the Condition

The LED changes according to the programmed condition.

Step 8 — Test

Add water gradually and observe how the sensor reading changes.

---

💻 Arduino Code

The following is a basic example for an analog soil moisture sensor and LED indicator:

int sensorPin = A0;
int ledPin = 7;

int sensorValue;

void setup() {
  Serial.begin(9600);

  pinMode(ledPin, OUTPUT);
}

void loop() {

  // Read soil moisture sensor
  sensorValue = analogRead(sensorPin);

  // Display reading
  Serial.print("Soil Moisture Value: ");
  Serial.println(sensorValue);

  // Check soil condition
  if (sensorValue > 500) {
    digitalWrite(ledPin, HIGH);
  }
  else {
    digitalWrite(ledPin, LOW);
  }

  delay(1000);
}

📝 Code Explanation

int sensorPin = A0;

Defines A0 as the analog input connected to the moisture sensor.

int ledPin = 7;

Defines digital pin 7 for the LED.

sensorValue = analogRead(sensorPin);

Reads the analog signal from the moisture sensor.

Serial.println(sensorValue);

Displays the sensor reading in the Arduino Serial Monitor.

if (sensorValue > 500)

Checks the reading against the selected threshold.

«Important: "500" is only an example threshold. You should calibrate the threshold using your own sensor and soil.»

---

🛠️ Setup Steps

1. Install Arduino IDE

Install the Arduino IDE on your computer.

2. Connect Arduino

Connect the Arduino Uno to the computer using a USB cable.

3. Build the Circuit

Connect:

Sensor VCC → Arduino 5V
Sensor GND → Arduino GND
Sensor AO  → Arduino A0
LED        → Arduino D7 through 220Ω resistor

4. Open the Arduino IDE

Create a new sketch.

5. Add the Code

Copy the Arduino code from this README into the Arduino IDE.

6. Select the Board

Select:

Arduino Uno

from the board selection menu.

7. Select the Port

Select the COM/serial port connected to your Arduino.

8. Upload the Program

Click Upload.

9. Open Serial Monitor

Open the Serial Monitor and set the baud rate to:

9600

10. Test the Sensor

Test the sensor in relatively dry soil and then gradually add water.

Observe how the sensor value changes.

---

🧪 Results

The project demonstrates that the soil moisture sensor can detect changes in soil condition and provide a corresponding signal to the Arduino.

During testing:

- The sensor produces different readings under different soil conditions.
- Arduino receives and processes the readings.
- The programmed threshold determines the output condition.
- The LED provides a simple visual indication.

Example Testing Table

Soil Condition| Sensor Reading*| Output
Relatively dry| High| LED indication
Partially moist| Medium| Depends on threshold
Wet/moist| Lower| LED indication

*Actual numerical values vary depending on the sensor, soil type, sensor placement, and calibration.

---

📸 Project Images

Recommended images for this repository:

1. Components Used

Show the Arduino Uno, soil moisture sensor, breadboard, jumper wires, LED and resistor.

Caption:

«Main electronic components used to build the Home Soil Moisture Detection System.»

2. Circuit Setup

Show the complete Arduino and sensor wiring.

Caption:

«Circuit setup showing the soil moisture sensor connected to the Arduino Uno and LED indicator.»

3. Sensor in Soil

Show the sensor inserted into the plant pot.

Caption:

«Soil moisture sensor placed inside the plant soil for real-time moisture detection.»

4. Testing

Show the Serial Monitor or the sensor being tested under different moisture conditions.

Caption:

«Testing the system by observing changes in sensor readings under different soil moisture conditions.»

5. Final Prototype

Show the complete working project beside the plant.

Caption:

«Final Home Soil Moisture Detection System prototype for smart gardening.»

---

🌿 Applications

This project can be used or extended for:

- 🪴 Home gardening
- 🌱 Indoor plants
- 🌿 Balcony gardens
- 🌾 Small-scale agriculture
- 🌳 Plant nurseries
- 🏡 Smart home gardening
- 💧 Smart irrigation
- 🏭 Greenhouse monitoring

---

🚀 Future Improvements

The current prototype can be upgraded into a more advanced smart gardening system.

💧 Automatic Irrigation

Add a relay and water pump so that watering can be controlled automatically.

Soil Sensor
     ↓
  Arduino
     ↓
   Relay
     ↓
 Water Pump
     ↓
    Plant

📡 IoT Connectivity

Use an ESP32 or ESP8266 to send sensor data over Wi-Fi.

📱 Mobile Monitoring

Display soil moisture information on a mobile application.

🔔 Notifications

Send an alert when the soil becomes too dry.

📊 Data Logging

Store moisture readings over time for analysis.

🖥️ LCD/OLED Display

Display the moisture condition locally without a computer.

🌦️ Multiple Sensors

Use multiple sensors to monitor several plants or different areas.

---

🎓 What I Learned

This project helped me develop practical knowledge in:

- Arduino programming
- Sensor interfacing
- Analog input reading
- Basic electronics
- Circuit connections
- Microcontroller programming
- Threshold-based control
- Testing and troubleshooting
- Automation concepts
- Smart agriculture applications

---

📁 Suggested Repository Structure

home-soil-moisture-detection-system/
│
├── README.md
│
├── code/
│   └── soil_moisture_detection.ino
│
├── images/
│   ├── 01-components.jpg
│   ├── 02-circuit-setup.jpg
│   ├── 03-sensor-in-soil.jpg
│   ├── 04-testing-results.jpg
│   └── 05-final-prototype.jpg
│
└── docs/
    └── project-notes.md

---

🔑 Keywords

Use these keywords as GitHub repository Topics:

soil-moisture
soil-moisture-sensor
arduino
arduino-uno
embedded-systems
iot
smart-gardening
smart-agriculture
smart-farming
soil-monitoring
sensor-interfacing
electronics-project
arduino-project
automation
home-automation
smart-irrigation
plant-monitoring
microcontroller

---

📌 Project Summary

Home Soil Moisture Detection System is a simple Arduino-based project that demonstrates how a soil moisture sensor can be combined with a microcontroller to monitor soil conditions.

The project provides practical experience in electronics, sensors, Arduino programming, automation, and smart gardening, while also providing a foundation for future IoT-based automatic irrigation systems.

---

👩‍💻 Project Type

Category: Arduino / Embedded Systems / Electronics
Application: Home Gardening & Smart Agriculture
Controller: Arduino Uno
Sensor: Soil Moisture Sensor
Output: LED / Serial Monitor
Level: Beginner-Friendly Electronics Project

---

⭐ Future Goal

«From simple soil monitoring to intelligent, automated and IoT-enabled gardening. 🌱🤖»

---

📜 License

This project is intended for educational and learning purposes. You are free to modify and improve the project for your own educational use.
