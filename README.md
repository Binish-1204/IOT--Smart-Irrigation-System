# IOT--Smart-Irrigation-System
An IoT-based system to monitor soil moisture, temperature, and humidity, with automated watering via a solenoid valve.

IOT - Smart Irrigation System
An IoT-based system to monitor soil moisture, temperature, and humidity, with automated watering via a solenoid valve. This project uses a NodeMCU ESP8266 to collect sensor data and control a water valve, with options to send data to either the Blynk or ThingSpeak cloud platform for remote monitoring.

# Circuit Diagram
Features
- Automated Watering: Activates a 24V solenoid valve to water plants when the soil moisture drops below a set threshold.
- Real-Time Data Monitoring: Streams live sensor data (temperature, humidity, soil moisture) to a cloud dashboard.
- Dual Cloud Support: Includes source code for integration with both Blynk (for interactive dashboards and notifications) and ThingSpeak (for data logging and graphing).
- Environment Sensing: Utilizes a DHT11 sensor for a complete overview of the plant's ambient conditions.

# Hardware Components
Component:                      Role in Project

NodeMCU ESP8266:                 The brain of the system; connects to Wi-Fi and controls components.

DHT11 Sensor    :                 Measures ambient air temperature and humidity.

Soil Moisture Sensor:             Detects the moisture level in the soil.

5V Relay Module      :            A safe switch to control the high-voltage solenoid valve with the low-voltage NodeMCU.

24V Solenoid Valve    :           The valve that physically opens or closes to control water flow.

24V Power Adapter      :          An external power supply specifically for the solenoid valve.

Breadboard          :             For creating and organizing the prototype circuit.

Jumper Wires         :            To connect all the electronic components.

Main Switch           :           (Optional but recommended) To safely turn power to the 24V adapter on/off.

# Software & Setup

1. Arduino IDE Configuration
Install Arduino IDE: Download from the official website.
Add ESP8266 Board Manager:
Go to File > Preferences.
In 'Additional Board Manager URLs', add: http://arduino.esp8266.com/stable/package_esp8266com_index.json
Install ESP8266 Boards:
Go to Tools > Board > Boards Manager.
Search for esp8266 and install the package.
Select NodeMCU 1.0 (ESP-12E Module) as your board.

2. Install Required Libraries
In the Arduino IDE, go to Sketch > Include Library > Manage Libraries and install:
Blynk by Volodymyr Shymanskyy
DHT sensor library by Adafruit
ThingSpeak by MathWorks

4. Code Configuration
Choose which version of the code you want to use:
- For Blynk (SmartPlantMonitoring.ino):
  Open the file in the Arduino IDE.
  Add your Wi-Fi credentials to the ssid and pass variables.
  Get an Auth Token from the Blynk app and add it to the auth variable.
  This code supports notifications and a control dashboard.

- For ThingSpeak (SmartPlantMonitoring2.ino):
  Open the file in the Arduino IDE.
  Add your Wi-Fi credentials.
  Create a ThingSpeak channel with two fields (for temperature and humidity).
  Add your Channel Number to myChannelNumber and Write API Key to myWriteAPIKey.
  This code is best for simple data logging.

4. Upload to NodeMCU
Connect your NodeMCU to your computer via USB.
Select the correct COM port under Tools > Port.
Click the "Upload" button.

# How It Works

The NodeMCU ESP8266 serves as the central controller. It periodically reads data from the soil moisture and DHT11 sensors.
- Data Collection: The microcontroller reads the analog value from the soil moisture sensor and the temperature/humidity from the DHT11.
- Cloud Communication: The data is then transmitted over Wi-Fi to the configured cloud platform (Blynk or ThingSpeak).
- Automated Watering Logic: The code checks if the soil moisture value has fallen below a predefined threshold.
- Valve Control: If the soil is too dry, the NodeMCU sends a HIGH signal to the 5V relay module. This closes the relay's switch, completing the separate 24V circuit and opening the solenoid valve. Water flows to the plants.
- Stopping Water Flow: Once the soil moisture level rises above the threshold, the NodeMCU sends a LOW signal to the relay, which opens the 24V circuit, closes the valve, and stops the watering.
