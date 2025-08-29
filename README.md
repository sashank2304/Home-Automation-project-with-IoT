## README.md

# Smart Home IoT Automation

## Overview

This project demonstrates **smart home automation** using IoT hardware controlled remotely with a mobile application via Bluetooth. The prototype allows remote access to household appliances (LEDs, servo motor for gates, and fans), using an ESP32 microcontroller and Android MIT App.[1]

## Features

- Remote control of appliances via smartphone app (Bluetooth)
- Control of two LED bulbs and one gate using servo motor
- Real-time monitoring and toggling with secure permissions
- Power-efficient automation using ESP32

## Motivation & Impact

- **Convenience**: Automates routine tasks like lighting and gate control
- **Efficiency**: Reduces energy waste through programmable logic
- **Safety & Security**: Enables remote monitoring and control
- **Societal Relevance**: Supports sustainability, aging in place, and smart city development[1]

## Hardware Requirements

| Component      | Specification        | Quantity |
|----------------|---------------------|----------|
| LED Bulb       | Standard LED bulb   | 2        |
| Servo Motor    | Compatible with gates| 1        |
| ESP-32S        | WiFi/Bluetooth       | 1        |

## System Design

- ESP32 communicates with a smartphone app using Bluetooth Serial
- Devices (LEDs, motor) respond to commands received via the app

## Getting Started

### Arduino Code

```cpp
#include "BluetoothSerial.h"
// init Class: 
BluetoothSerial ESP_BT;

// init PINs:
int led_pin_1 = 4; 
int led_pin_2 = 2; 

int incoming; 

void setup() {
  Serial.begin(19200);
  ESP_BT.begin("ESP32_Control");
  pinMode (led_pin_1, OUTPUT);
  pinMode (led_pin_2, OUTPUT);
}

void loop() {
  if (ESP_BT.available()) {
    incoming = ESP_BT.read();
    int button = floor(incoming / 10);
    int value = incoming % 10;
    switch (button) {
      case 1:
        Serial.print("Button 1:"); Serial.println(value);
        digitalWrite(led_pin_1, value);
        break;
      case 2:
        Serial.print("Button 2:"); Serial.println(value);
        digitalWrite(led_pin_2, value);
        break;
    }
  }
}
```


### MIT App

- Develop the control interface using MIT App Inventor or equivalent mobile platform
- Set Bluetooth device permissions

## Troubleshooting

If Bluetooth devices fail to connect, verify the app has “Nearby devices” permissions enabled in the phone’s settings.

 ## Future Scope

- Expanded device connectivity
- AI/ML for predictive automation
- Enhanced security and sustainability features

 ## License

This project is licensed under the MIT License.

## Authors

- Amrit Reddy
- Samvrudha R.R.
- Sashank Abburu



This setup covers everything needed to launch your GitHub repository and accurately document your smart home IoT automation solution.[1]

[1](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/90786489/b2053064-bf9f-485d-9688-f98358f96f8b/Final-iot-report.pdf)
