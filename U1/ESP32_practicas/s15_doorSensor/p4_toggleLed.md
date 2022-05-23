# ESP32 - Door Sensor Toggle LED

This tutorial instructs you how to use ESP32 to toggle LED each time door is closed.

## Hardware Used In This Tutorial

  * 1	×	ESP-WROOM-32 Dev Module	
  * 1	×	Micro USB Cable	
  * 1	×	Door Sensor	
  * 1	×	LED	
  * 1	×	220 ohm resistor	
  * 1	×	Breadboard	
  * 4	×	Jumper Wires

---

## Wiring Diagram

![](figs/fig_4_1.jpg)

## ESP32 Code - Door Sensor Toggles LED

```c++
#define DOOR_SENSOR_PIN  23  // ESP32 pin GIOP23 connected to the OUTPUT pin of door sensor
#define LED_PIN          17  // ESP32 pin GIOP17 connected to LED's pin

// The below are variables, which can be changed
int ledState = LOW;   // the current state of LED
int lastDoorState;    // the previous state of door sensor
int currentDoorState; // the current state of door sensor

void setup() {
  Serial.begin(9600);                     // initialize serial
  pinMode(DOOR_SENSOR_PIN, INPUT_PULLUP); // set ESP32 pin to input pull-up mode
  pinMode(LED_PIN, OUTPUT);               // set ESP32 pin to output mode

  currentDoorState = digitalRead(DOOR_SENSOR_PIN);
}

void loop() {
  lastDoorState    = currentDoorState;             // save the last state
  currentDoorState = digitalRead(DOOR_SENSOR_PIN); // read new state

  if (lastDoorState == HIGH && currentDoorState == LOW) { // state change: HIGH -> LOW
    Serial.println("The door-closing event is detected, toggles the state of LED");

    // toggle state of LED
    ledState = !ledState;

    // control LED arccoding to the toggled state
    digitalWrite(LED_PIN, ledState);
  }
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
  * Move the magnet close to the reed switch and them move it far from the reed switch. Repeat this several times
  * See the change of LED's state


