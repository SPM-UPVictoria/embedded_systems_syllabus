# ESP32 Post request

```c++
#include <Arduino.h>
#include <WiFi.h>
#include <HTTPClient.h>
#include <DHT_U.h>
#include <DHT.h>

#define dhtPin 21
#define DHT_SENSOR_TYPE DHT22


const char* ssid = "red_de_becarios";
const char* password = "hola_soy_becario";

const char* serverName = "http://192.168.0.104/esp32/insert_temp_hum.php";

unsigned long lastTime = 0;
unsigned long timerDelay = 10000;

float humi = 0;
float temp = 0;

DHT dht_sensor(dhtPin, DHT_SENSOR_TYPE);

void setup() {
  Serial.begin(115200);

  WiFi.begin(ssid, password);

  Serial.println("Connecting");
  while(WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.print("Connected to WiFi network with IP Address: ");
  Serial.println(WiFi.localIP());

  dht_sensor.begin();
}

void loop() {
  if ((millis() - lastTime) > timerDelay) {
    if(WiFi.status()== WL_CONNECTED){
      WiFiClient client;
      HTTPClient http;

      humi = dht_sensor.readHumidity();
      temp = dht_sensor.readTemperature();

      if (isnan(temp) || isnan(humi)) {
        Serial.println("Failed to read from DHT sensor");
      } else {
        http.begin(client, serverName);

        // Specify content-type header
        http.addHeader("Content-Type", "application/x-www-form-urlencoded");
        // Data to send with HTTP POST
        String httpRequestData = "temperature=" + String(temp, 6) + "&humidity=" + String(humi, 6);
        // Send HTTP POST request
        int httpResponseCode = http.POST(httpRequestData);
        
        // If you need an HTTP request with a content type: application/json, use the following:
        //http.addHeader("Content-Type", "application/json");
        //int httpResponseCode = http.POST("{\"api_key\":\"tPmAT5Ab3j7F9\",\"sensor\":\"BME280\",\"value1\":\"24.25\",\"value2\":\"49.54\",\"value3\":\"1005.14\"}");

        // If you need an HTTP request with a content type: text/plain
        //http.addHeader("Content-Type", "text/plain");
        //int httpResponseCode = http.POST("Hello, World!");

        Serial.print("HTTP Response code: ");
        Serial.println(httpResponseCode);
          
        // Free resources
        http.end();
      }

    
    } else {
      Serial.println("WiFi Disconnected");
    }

    lastTime = millis();
  }
}
```

## Página de recepción de datos en PHP

```php
<?php

    $conn = new mysqli("127.0.0.1", "esp32_admi", "sctAPWE_#F|PhzX%", "esp32");

    if ($conn->connect_error) {
        echo "Error:" . $conn->connect_error . PHP_EOL;
        die();
    }

    $temp = floatval($_POST["temperature"]);
    $hum = floatval($_POST["humidity"]);

    $query = "INSERT INTO temp_hum(t, h) VALUES ($temp, $hum)";

    echo $query . PHP_EOL;

    if ($conn->query($query) === TRUE) {
        echo "Done";
    } else {
        echo "Error: " . $conn->error;
    }

    $conn->close();
?>

```