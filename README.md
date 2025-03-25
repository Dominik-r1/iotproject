# Automatic Plant Watering System

## Overview
This project is an **Automatic Plant Watering System** using an **Arduino Uno**, a **soil moisture sensor**, a **relay module**, and a **water pump**. The system detects the moisture level in the soil and automatically waters the plant when the soil is dry. The code is also designed to work in the **Wokwi Simulator**.

## Components Used
- **Arduino Uno** (Microcontroller)
- **Soil Moisture Sensor with Comparison Module** (Detects moisture levels)
- **Relay Module** (Controls the water pump)
- **Water Pump (5V or 12V DC)** (Waters the plant)
- **Battery Pack** (Powers the system)
- **LED (Simulating the Pump in Wokwi)**

## How It Works
1. The **soil moisture sensor** reads the moisture level in the soil.
2. The **comparison module** gives a **HIGH (1) or LOW (0) output** based on the soil moisture.
3. If the soil is **dry** (LOW signal), the **relay turns ON**, activating the **water pump**.
4. If the soil is **moist** (HIGH signal), the **relay turns OFF**, stopping the **water pump**.
5. In the **Wokwi simulator**, an **LED is used instead of a water pump** to indicate when the pump is ON/OFF.

## Code Explanation

const int sensorPin = 2;  // Digital Output from Comparison Module
const int relayPin = 7;   // Relay Module Connected to Digital Pin 7
const int pumpLED = 13;   // LED to simulate pump (for Wokwi)

void setup() {
  pinMode(sensorPin, INPUT);  // Soil sensor as input
  pinMode(relayPin, OUTPUT);  // Relay module as output
  pinMode(pumpLED, OUTPUT);   // Simulated pump (LED)
  
  digitalWrite(relayPin, HIGH); // Ensure relay is OFF at startup
  digitalWrite(pumpLED, LOW);   // Ensure LED is OFF at startup
  
  Serial.begin(9600);
}

void loop() {
  int soilState = digitalRead(sensorPin); // Read sensor state
  
  Serial.print("Soil Moisture Status: ");
  Serial.println(soilState);

  if (soilState == LOW) {  // Soil is DRY (LOW signal from sensor)
    digitalWrite(relayPin, LOW); // Turn ON the relay
    digitalWrite(pumpLED, HIGH); // Simulated pump ON
    Serial.println("Watering the plant...");
  } else {  // Soil is WET (HIGH signal from sensor)
    digitalWrite(relayPin, HIGH); // Turn OFF the relay
    digitalWrite(pumpLED, LOW);   // Simulated pump OFF
    Serial.println("Soil is moist. Pump is OFF.");
  }

  delay(5000); // Check every 5 seconds
}


## How to Simulate in Wokwi
1. Go to [Wokwi](https://wokwi.com/).
2. Select **"New Project" > "Arduino Uno"**.
3. Add the following components:
   - **Push Button (Simulates moisture sensor output)**
   - **Relay Module**
   - **LED (Simulating Water Pump)**
4. Copy and paste the code into Wokwi and run the simulation.

## Future Enhancements
- Integrate **ESP8266 or ESP32** for remote monitoring via WiFi.
- Send moisture data to **Google Sheets** for logging.
- Add an **LCD display** to show moisture levels.
- Use a **solar-powered battery** for sustainability.


