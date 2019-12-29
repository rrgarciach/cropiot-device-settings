# CropIoT Device Settings Library

This a Arduino/NodeMCU compatible library to provide device settings setup out of the box through a REST API and SPA UI.

## Installation using PlatformIO:
- Add library dependency at `platformio.ini` file:
```
lib_deps =
  https://github.com/rrgarciach/cropiot-device-settings.git
```
- Add include line in your `main.cpp`:
```
#include "CropIoTDeviceSettings.h"
```
- Declare the name of your device inside `setup()`. This name will be used as the Access Point name as well:
```
void setup() {
  DEVICE_TYPE = "my_device_name";
  ...
```
- Start Serial and run function to connect WiFi inside `setup()`:
```
  Serial.begin(115200);
  Serial.println("Starting...");

  connectWiFi();
```
- Generate any required WLAN:
```
  wlanClient1 = generateWiFiClient();
  connectMQTT(mqttClient1);
```
- Add any required device custom endpoints as `/include/device_endpoints.h`
(and include them using `#include "../include/device_endpoints.h"`) with content similar as follows:
```
#ifndef DEVICE_ENDPOINTS_H_
#define DEVICE_ENDPOINTS_H_

// Device setup endpoints
struct {
  struct {
    struct  {
      const char* PH_CALIBRATE = "/api/device/ph/calibrate";
      const char* EC_CALIBRATE = "/api/device/ec/calibrate";
    } DEVICE;
  } API;
} DEVICE_URLS;

#endif
```

### Dependencies

- https://github.com/me-no-dev/ESPAsyncWebServer.git
- https://github.com/me-no-dev/arduino-esp32fs-plugin.git
- https://github.com/bblanchon/ArduinoJson.git#5.x
- https://github.com/knolleary/pubsubclient.git

### Additional hints
To upload static files from `/data` directory simply run:
`pio run -t uploadfs`

### Additional documentation
https://github.com/esp8266/Arduino/blob/master/doc/esp8266wifi/station-class.rst
https://github.com/knolleary/pubsubclient/blob/master/examples/mqtt_esp8266/mqtt_esp8266.ino
