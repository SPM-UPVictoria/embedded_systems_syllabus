# ESP32 - Light Sensor Triggers LED

This tutorial instructs you how to use ESP32, light sensor and LED to do a project that:

  * Turns LED on if the analog value measured from light sensor's is below a threshold,
  * Turns LED off if the analog value measured from light sensor's is above a threshold,

## Hardware Used In This Tutorial

  * 1	×	ESP-WROOM-32 Dev Module	
  * 1	×	Micro USB Cable	
  * 1	×	Light Sensor	
  * 1	×	LED	
  * 1	×	220 ohm resistor	
  * 1	×	10 kΩ resistor	
  * 1	×	Breadboard	
  * n	×	Jumper Wires

## Wiring Diagram

![](figs/fig_2_1.jpg)

## ESP32 Code

```c++
// The below are constants, which cannot be changed
#define LIGHT_SENSOR_PIN  36  // ESP32 pin GIOP36 (ADC0) connected to light sensor
#define LED_PIN           22  // ESP32 pin GIOP22 connected to LED
#define ANALOG_THRESHOLD  500

void setup() {
  pinMode(LED_PIN, OUTPUT); // set ESP32 pin to output mode
}

void loop() {
  int analogValue = analogRead(LIGHT_SENSOR_PIN); // read the value on analog pin

  if (analogValue < ANALOG_THRESHOLD)
    digitalWrite(LED_PIN, HIGH); // turn on LED
  else
    digitalWrite(LED_PIN, LOW);  // turn off LED
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
  * Radiates light to sensor
  * See the change of LED's state


