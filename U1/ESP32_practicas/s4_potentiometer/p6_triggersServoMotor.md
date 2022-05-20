# ESP32 - Potentiometer Triggers Servo Motor

This tutorial instructs you how to use ESP32 with the potentiometer to control servo motor. In detail:

  * The ESP32 automatically rotates a servo motor to 90° if the potentiometer's analog value is above a threshold
  * The ESP32 automatically rotates a servo motor to back to 0° if the potentiometer's analog value is under a threshold

We also learn how to convert the analog value to voltage and then use the voltage threshold to control the LED:

  * The ESP32 automatically rotates a servo motor to 90° if the potentiometer's voltage is above a threshold.
  * The ESP32 automatically rotates a servo motor back to 0° if the potentiometer's voltage is under a threshold.

## Hardware Used In This Tutorial

  * 1	×	ESP-WROOM-32 Dev Module	
  * 1	×	Micro USB Cable	
  * 1	×	Potentiometer	
  * 1	×	Servo Motor	
  * n	×	Jumper Wires

---

## Wiring Diagram

![](figs/fig_6_1.jpg)

## ESP32 Code - Analog Threshold

```c++
#include <Servo.h>

#define POTENTIOMETER_PIN  36  // ESP32 pin GIOP36 (ADC0) connected to Potentiometer pin
#define SERVO_PIN          26  // ESP32 pin GIOP26 connected to Servo Motor's pin
#define ANALOG_THRESHOLD   1000

Servo servo; // create servo object to control a servo

void setup() {
  servo.attach(SERVO_PIN);   // attaches the servo on pin 9 to the servo object
  servo.write(0);
}

void loop() {
  int analogValue = analogRead(POTENTIOMETER_PIN); // read the input on analog pin

  if (analogValue > ANALOG_THRESHOLD)
    servo.write(90); // rotate servo motor to 90 degree
  else
    servo.write(0);  // rotate servo motor to 0 degree
}

```

### Quick Instructions

  * If this is the first time you use ESP32, see how to setup environment for ESP32 on Arduino IDE.
  * Do the wiring as above image.
  * Connect the ESP32 board to your PC via a micro USB cable
  * Open Arduino IDE on your PC.
  * Select the right ESP32 board (e.g. ESP32 Dev Module) and COM port.
  * Copy the above code and paste it to Arduino IDE.
  * Compile and upload code to ESP32 board by clicking Upload button on Arduino IDE
  * Rotate the potentiometer
  * See servo motor rotating

---

## ESP32 Code - Voltage Threshold

The analog value read from the potentiometer is converted to voltage, and then the voltage is compared to a voltage threshold. If it exceeds the threshold, it triggers a servo motor

```c++
#include <Servo.h>

#define POTENTIOMETER_PIN  36  // ESP32 pin GIOP36 (ADC0) connected to Potentiometer pin
#define SERVO_PIN          26  // ESP32 pin GIOP26 connected to Servo Motor's pin
#define VOLTAGE_THRESHOLD  2.5 // Voltages

Servo servo; // create servo object to control a servo

void setup() {
  servo.attach(SERVO_PIN);   // attaches the servo on pin 9 to the servo object
  servo.write(0);
}

void loop() {
  int analogValue = analogRead(POTENTIOMETER_PIN);      // read the input on analog pin
  float voltage = floatMap(analogValue, 0, 1023, 0, 5); // Rescale to potentiometer's voltage

  if (voltage > VOLTAGE_THRESHOLD)
    servo.write(90); // rotate servo motor to 90 degree
  else
    servo.write(0);  // rotate servo motor to 0 degree
}

float floatMap(float x, float in_min, float in_max, float out_min, float out_max) {
  return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min;
}

```

### Quick Instructions

  * If this is the first time you use ESP32, see how to setup environment for ESP32 on Arduino IDE.
  * Do the wiring as above image.
  * Connect the ESP32 board to your PC via a micro USB cable
  * Open Arduino IDE on your PC.
  * Select the right ESP32 board (e.g. ESP32 Dev Module) and COM port.
  * Copy the above code and paste it to Arduino IDE.
  * Compile and upload code to ESP32 board by clicking Upload button on Arduino IDE
  * Rotate the potentiometer
  * See servo motor rotating

