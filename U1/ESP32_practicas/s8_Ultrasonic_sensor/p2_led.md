# SP32 - Ultrasonic Sensor - LED

This tutorial instructs you how to use ESP32 and Ultrasonic sensor to control the LED. In detail:

  * The ESP32 automatically turns LED on when an object is close to the ultrasonic sensor.
  * The ESP32 automatically turns LED off when an object is far from the ultrasonic sensor.

## Hardware Used In This Tutorial

  * 1	×	ESP-WROOM-32 Dev Module	
  * 1	×	Micro USB Cable	
  * 1	×	Ultrasonic Sensor	
  * 1	×	LED	
  * 1	×	220 ohm resistor	
  * 1	×	Breadboard	
  * 4	×	Jumper Wires

---

Wiring Diagram

The wiring diagram with power supply from USB cable

![](figs/fig_2_1.jpg)

The wiring diagram with power supply from 5v adapter

![](figs/fig_2_2.jpg)

## ESP32 Code

```c++
#define TRIG_PIN  26 // ESP32 pin GIOP26 connected to Ultrasonic Sensor's TRIG pin
#define ECHO_PIN  25 // ESP32 pin GIOP25 connected to Ultrasonic Sensor's ECHO pin
#define LED_PIN   17 // ESP32 pin GIOP17 connected to LED's pin
#define DISTANCE_THRESHOLD 50 // centimeters

// The below are variables, which can be changed
float duration_us, distance_cm;

void setup() {
  Serial.begin (9600);       // initialize serial port
  pinMode(TRIG_PIN, OUTPUT); // set ESP32 pin to output mode
  pinMode(ECHO_PIN, INPUT);  // set ESP32 pin to input mode
  pinMode(LED_PIN, OUTPUT);  // set ESP32 pin to output mode
}

void loop() {
  // generate 10-microsecond pulse to TRIG pin
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // measure duration of pulse from ECHO pin
  duration_us = pulseIn(ECHO_PIN, HIGH);
  // calculate the distance
  distance_cm = 0.017 * duration_us;

  if (distance_cm < DISTANCE_THRESHOLD)
    digitalWrite(LED_PIN, HIGH); // turn on LED
  else
    digitalWrite(LED_PIN, LOW);  // turn off LED

  // print the value to Serial Monitor
  Serial.print("distance: ");
  Serial.print(distance_cm);
  Serial.println(" cm");

  delay(500);
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
  * Move your hand in front of sensor
  * See the change of LED's state