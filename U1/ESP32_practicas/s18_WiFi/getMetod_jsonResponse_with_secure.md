# ESP32 Get Method + JSON response

```c++
#include <Arduino.h>
#include <WiFi.h>
#include <WiFiClientSecure.h>
#include <HTTPClient.h>
#include <Arduino_JSON.h>


const char* ssid = "red_de_becarios";
const char* password = "hola_soy_becario";

const char* serverName = "https://api.sunrise-sunset.org/json?lat=23.729425&lng=-99.076868&date=today";
const int port = 443;

unsigned long lastTime = 0;
unsigned long timerDelay = 5000;

String JSONResponse;

WiFiClientSecure client;

const char* root_ca = \
"-----BEGIN CERTIFICATE-----\n" \
"MIIFMzCCBBugAwIBAgISA7RYDqFcNgG4qBlC5rEOSmggMA0GCSqGSIb3DQEBCwUA\n" \
"MDIxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbmNyeXB0MQswCQYDVQQD\n" \
"EwJSMzAeFw0yMjA0MjMyMjI5MzJaFw0yMjA3MjIyMjI5MzFaMCExHzAdBgNVBAMT\n" \
"FmFwaS5zdW5yaXNlLXN1bnNldC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAw\n" \
"ggEKAoIBAQDoSowkdUY/c1rmz1wzSk6SW8S5EIiTZMrKjpLzGftzqcRDbGOQdRpu\n" \
"qZdSzenJQXYUKUp0DrtRim7EmO+ymINahNzkhFEXBE4CFg6bz6/WXOPfZgcaj2Sp\n" \
"0JWC5T6fexjG7PCbV9jK8bJAyaYqvYMpDwq87ltcT2zkRlrullw2dBEx4jG72Oce\n" \
"CB5ClHz/sDeg/+QfkqNWoNMMLeh2WREKQpO+p93rqiWYWkqKhHXRF1jHdYU6yiAy\n" \
"p5dfc3cqNB4cU5wKaMNk0SRB6mlUwuCPVaFtVKzpWzoa4whsoW69p0tc4oahFxJr\n" \
"OpoxluUAA7BHo8xX4Q8Ukob2ZQVKRXVpAgMBAAGjggJSMIICTjAOBgNVHQ8BAf8E\n" \
"BAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMAwGA1UdEwEB/wQC\n" \
"MAAwHQYDVR0OBBYEFP+UMLIIe+5XUo1grBnH8MGE+8bnMB8GA1UdIwQYMBaAFBQu\n" \
"sxe3WFbLrlAJQOYfr52LFMLGMFUGCCsGAQUFBwEBBEkwRzAhBggrBgEFBQcwAYYV\n" \
"aHR0cDovL3IzLm8ubGVuY3Iub3JnMCIGCCsGAQUFBzAChhZodHRwOi8vcjMuaS5s\n" \
"ZW5jci5vcmcvMCEGA1UdEQQaMBiCFmFwaS5zdW5yaXNlLXN1bnNldC5vcmcwTAYD\n" \
"VR0gBEUwQzAIBgZngQwBAgEwNwYLKwYBBAGC3xMBAQEwKDAmBggrBgEFBQcCARYa\n" \
"aHR0cDovL2Nwcy5sZXRzZW5jcnlwdC5vcmcwggEFBgorBgEEAdZ5AgQCBIH2BIHz\n" \
"APEAdgApeb7wnjk5IfBWc59jpXflvld9nGAK+PlNXSZcJV3HhAAAAYBYwlThAAAE\n" \
"AwBHMEUCIQDtdXBBQK776Yjfj0RVDZQO0Z2dHeG2ulMKBbAUbYaURAIgGpIwqOww\n" \
"8wyvTqQmudaBJ7DAqllbmhftDL2ohR31d/kAdwBvU3asMfAxGdiZAKRRFf93FRwR\n" \
"2QLBACkGjbIImjfZEwAAAYBYwlUTAAAEAwBIMEYCIQCalzaVMjtSQWD8XJrAQxdP\n" \
"HouWW+e0sXsBG1xyO66S9QIhAJjx6QEFPrJw2yji7RhTc9ufcAB1+886lWmcY57y\n" \
"uqiEMA0GCSqGSIb3DQEBCwUAA4IBAQAybYf43hOuvyg/yfX17x6Q8fLmLuuB2Mc0\n" \
"XsoWFSjdLPlE+NiYEw7iQegj71IZlxXTqr0bs3sBNaf7sdZ//ThugfYHyCVWyCNq\n" \
"Rvyy3RZJYp9plIkIP/EIOmQBXwY5qIGhx0It6nDtsjZ04Q3tW/OYb5kxuasX4Mu+\n" \
"Elfhh/uNaAWK3Wq3jl4B7j92A64+IebcSrsGXIunTZU4aCqVK7IFEbjcbT5xlmqg\n" \
"wM6l3Cm6l65AV+0mm3qmQYrlQ1QH+vtdO5kc2LODu4kb2Qgqjj0CnI/2i+5pjYWU\n" \
"wwe3/JFQY53ThtWZharEO6XqW0pZW3cWx/aMbTQKEwsP7IJ5CgCc\n" \
"-----END CERTIFICATE-----\n";

String httpGetRequest(const char* serverName) {
  HTTPClient http;

  http.begin(serverName);

  int httpResponseCode = http.GET();

  String payLoad = "{}";

  if (httpResponseCode>0) {
    Serial.print("HTTP Response code: ");
    Serial.println(httpResponseCode);
    payLoad = http.getString();
  } else {
    Serial.print("Error code: ");
    Serial.println(httpResponseCode);
  }
  // free resources
  http.end();

  return payLoad;
}

void setup() {
  Serial.begin(115200);

  WiFi.begin(ssid, password);
  Serial.print("\nConnecting ");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("");
  Serial.print("Connected to WiFi network with IP Address");
  Serial.println(WiFi.localIP());
  client.setCACert(root_ca);
  delay(2000);
}

void loop() {
  if ((millis() - lastTime) > timerDelay) {
    if (WiFi.status() == WL_CONNECTED) {
      JSONResponse = httpGetRequest(serverName);

      Serial.println(JSONResponse);
      JSONVar myObject = JSON.parse(JSONResponse);

      if (JSON.typeof(myObject) == "undefined") {
        Serial.println("Parsing input failed!");
        return;
      }

      Serial.print("JSON object =");
      Serial.println(myObject);

      // myObject.keys() can be used to get an array of all the keys in the object
      JSONVar keys = myObject.keys();

      for (int i=0; i < keys.length(); i++) {
        JSONVar value = myObject[keys[i]];
        Serial.print(keys[i]);
        Serial.print(" = ");
        Serial.println(value);
      }
    } else {
      Serial.println("WiFi Disconnected");
    }
    lastTime = millis();
  }
}
```