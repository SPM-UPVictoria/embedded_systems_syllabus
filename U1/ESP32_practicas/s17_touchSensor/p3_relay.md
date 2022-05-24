# ESP32 - Touch Sensor - Relay

his tutorial instructs you how to use ESP32 to control LED based on the state of the touch sensor. In detail:

  * If a touch sensor is being touched, ESP32 activates a relay
  * If a touch sensor is NOT being touched, ESP32 deactivates a relay

We can extend this tutorial to use the touch sensor to control a led strip, siren, light bulb, or motor... by connnecting them to the relay.

## Hardware Used In This Tutorial

  * 1	×	ESP-WROOM-32 Dev Module	
  * 1	×	Micro USB Cable	
  * 1	×	Touch Sensor	
  * 1	×	Relay	
  * 1	×	Warning Light Bright Waterproof	
  * 1	×	12V Power Adapter	
  * n	×	Jumper Wires

---

## Wiring Diagram

![](figs/fig_3_1.jpg)

## ESP32 Code

```c++
#define TOUCH_SENSOR_PIN  22 // ESP32 pin GIOP22 connected to touch sensor's pin
#define RELAY_PIN         27 // ESP32 pin GIOP27 connected to relay's pin

void setup() {
  Serial.begin(9600);               // initialize serial
  pinMode(TOUCH_SENSOR_PIN, INPUT); // set ESP32 pin to input mode
  pinMode(RELAY_PIN, OUTPUT);       // set ESP32 pin to output mode
}

void loop() {
  int touchState = digitalRead(TOUCH_SENSOR_PIN); // read new state

  if (touchState == HIGH) {
    Serial.println("The sensor is being touched");
    digitalWrite(RELAY_PIN, HIGH); // turn on
  } else if (touchState == LOW) {
    Serial.println("The sensor is untouched");
    digitalWrite(RELAY_PIN, LOW);  // turn off
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
  * Touch and keep touching the touch sensor several seconds
  * See the change of relay's state


