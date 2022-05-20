# ESP32 - Ultrasonic Sensor

This tutorial instructs you how to use ESP32 with the ultrasonic sensor HC-SR04 to measure the distance.

## Hardware Used In This Tutorial

  * 1	×	ESP-WROOM-32 Dev Module	
  * 1	×	Micro USB Cable	
  * 1	×	Ultrasonic Sensor	
  * 4	×	Jumper Wires

---

## Introduction to Ultrasonic Sensor

The ultrasonic sensor HC-SR04 is used to measure the distance from the sensor to an object by using ultrasonic waves.

### Ultrasonic Sensor Pinout

The ultrasonic sensor HC-SR04 includes four pins:

  * **VCC pin**: connect this pin to VCC (5V)
  * **GND pin**: connect this pin to GND (0V)
  * **TRIG pin**: this pin receives a control pulse from ESP32.
  * **ECHO pin**: this pin generates a pulse corresponding to the measured distance to ESP32.

