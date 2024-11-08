# House Automation IoT Project: ESP32 with DHT Sensor, Servo, and WS2812 LED Control

## Overview

This project utilizes an ESP32 microcontroller to monitor temperature and humidity data from a DHT22 sensor, control a WS2812 LED strip, and operate a servo motor for various automation tasks. The data is sent to a Node-RED dashboard via MQTT, allowing for real-time monitoring and control. This system can be used for automating different functions in a house, such as controlling lighting, climate, and device positioning.

## Features

- **Real-Time Temperature and Humidity Monitoring**: Continuously measures temperature and humidity using a DHT22 sensor.
- **LED Control**: Turn on/off an onboard LED via MQTT.
- **WS2812 LED Strip**: Set RGB colors on a WS2812 LED strip to control lighting.
- **Servo Motor Control**: Rotate the servo motor to adjust home devices like curtains, blinds, or vents.
- **MQTT Integration**: All controls and monitoring data are sent over MQTT for easy IoT integration.
- **Node-RED Dashboard**: Customizable dashboard for visualizing environmental data and sending commands for automation.

## Hardware and Software Components

- **ESP32**: Microcontroller with WiFi capability.
- **DHT22 Sensor**: Digital humidity and temperature sensor for environmental monitoring.
- **WS2812 LED Strip**: RGB LED strip with individually addressable LEDs for ambient lighting.
- **Servo Motor**: Basic servo motor for adjusting angles of home automation devices (e.g., blinds, doors).
- **Node-RED**: Used for the IoT dashboard to control and visualize data.
- **Wokwi Simulation**: Used for simulating the ESP32 and components.

## Setup and Configuration

### Hardware Connections

| Component            | Pin on ESP32 | Notes                              |
|----------------------|--------------|------------------------------------|
| DHT22 Sensor         | GPIO 2       | Temperature and humidity data     |
| LED (Onboard)        | GPIO 32      | LED controlled via MQTT           |
| Servo Motor          | GPIO 22      | Angle controlled via MQTT         |
| WS2812 LED Strip     | GPIO 5       | RGB color control                 |

### Libraries Required

- **Adafruit Sensor**: For interfacing with DHT22.
- **DHT_U**: Unified sensor library for DHT.
- **WiFi.h**: Built-in ESP32 WiFi library.
- **PubSubClient**: MQTT library.
- **ESP32Servo**: Servo motor control.
- **FastLED**: WS2812 LED strip control.

To install these libraries, go to the Arduino IDE Library Manager.

### WiFi and MQTT Setup

In the code, replace `ssid` and `password` with your WiFi credentials, and `mqttServer` with your MQTT broker address (e.g., `broker.hivemq.com` for public testing).

## Code Explanation

### `setup()`

The `setup()` function initializes all components and connects the ESP32 to the WiFi and MQTT broker. The MQTT callback function (`callback`) is set up here to handle incoming messages for automation tasks like controlling the LED, servo, and LED strip.

### `loop()`

The `loop()` function handles:

- **MQTT Connection**: Reconnects if the connection is lost.
- **Sensor Readings**: Reads temperature and humidity values from the DHT22 sensor.
- **MQTT Publishing**: Publishes sensor readings to the MQTT topic (`Tempdata`).

### Callback Function

The `callback()` function processes messages received via MQTT:

- **"lights" Topic**: Controls the onboard LED.
- **"servo" Topic**: Moves the servo to the specified angle.
- **"lights/neopixel" Topic**: Changes the WS2812 LED strip color using RGB values sent in the format "R,G,B".

## Node-RED Integration

Set up a Node-RED flow that subscribes to the following MQTT topics:

- **Tempdata**: For temperature and humidity data.
- **lights**: To control the onboard LED.
- **servo**: For setting servo angle.
- **lights/neopixel**: For setting the WS2812 LED strip color.

The dashboard can be designed to display:

- Real-time temperature and humidity readings.
- Buttons for turning the LED on/off.
- A color picker for the WS2812 LED strip.
- A slider or number input for setting the servo angle.

## Simulation with Wokwi

This project can be simulated in [Wokwi](https://wokwi.com) using the ESP32, DHT22, WS2812 LED, and servo components available. You can directly upload this code to test the MQTT communication, temperature/humidity readings, and control features.

## Sample MQTT Commands

Here are some MQTT messages you can send to test the project:

- **Turn on LED**: Publish "ON" to `lights`.
- **Turn off LED**: Publish "OFF" to `lights`.
- **Set Servo Angle**: Publish "90" to `servo` (or any other angle between 0-180).
- **Set NeoPixel Color**: Publish "255,0,0" to `lights/neopixel` for red, "0,255,0" for green, etc.

## Future Enhancements

Consider adding:

- Additional sensors for more data monitoring (e.g., motion sensor, air quality sensor).
- More control options for servo or LED behavior.
- A dynamic web-based dashboard for remote access.
- Integration with other home automation systems (e.g., Google Home, Amazon Alexa).

## License

This project is open-source and distributed under the [MIT License](LICENSE). Feel free to use and modify it as needed.

