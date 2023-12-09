# SmartCamera_Nutpapop
Controlling Zigbee LED light with hand gestures using ESP-32 CAM and Node-RED with Python CVZone.
This project is intended to be used in a linux environment.

## Contributors
1. Nutpapop Yasawut
2. Kasidit Chunpen

# Installation
## Prerequisites
- Softwares
  1. Python *3.10*
  2. Docker
  3. Node.js *16*
  4. Node-RED
  5. Visual Studio Code with PlatformIO Extension
  6. Zigbee2MQTT
- Hardwares
  1. Computer with Linux based Operating System
  2. ESP32-CAM
  3. Zigbee USB Dongle

## Clone this repository
```bash
git clone https://github.com/CprE-KMUTNB/SmartCamera_Nutpapop.git
cd SmartCamera_Nutpapop
```

## ESP-32 CAM
### Change configurations as needed in `src/platform-io/Esp32CamWebserver/src/CameraWebsocket.cpp`
```cpp
...
IPAddress LocalIp(192, 168, 1, 200);
IPAddress Gateway(192, 168, 1, 1);
IPAddress NMask(255, 255, 255, 0);
...
const char *hotspot_ssid = "ESP32-CAM";
const char *hotspot_password = "12345678";
...
const uint16_t websockets_server_port = 8000; // OPTIONAL CHANGE
...
```
### Upload the PlatformIO project in `src/platform-io/Esp32CamWebserver`

## Linux
### Configure and start Zigbee2MQTT
### Pair the LED with Zigbee2MQTT
### Make a python virtual environment and install packages
```bash
python -m venv ./venv
source venv/bin/activate
pip install -r requirements.txt
```
### Create a Docker container with `eclipse-mosquitto` image
```bash
docker run -it -p 1883:1883 -p 9001:9001 -v mosquitto.conf:/mosquitto/config/mosquitto.conf eclipse-mosquitto
```
### Change configurations as needed in `settings.conf`
### Run the start script
```bash
./bin/start.sh
```

# Usage
## Initial Configuration
- Connect to ESP32-CAM hotspot with the configured password
- Go to `192.168.1.200` in web browser
- Configure WiFi and Node-RED server IP Address
- Go to `http://localhost:1880/ui` in web browser

## Modes of Operation
### Mode 1 (Default)
| Fingers           | Operation        |
|-------------------|------------------|
| 1 fingers up      | Toggle ON/OFF    |
| 2 fingers up      | MODE Brightness  |
| 3 fingers up      | MODE Temperature |
| 4 fingers up      | MODE Color       |
### Mode 2 (Brightness)
| Fingers                   | Operation                          |
|---------------------------|------------------------------------|
| 1 to 5 fingers up         | Incrementally set brightness level |
| Index finger and Pinky up | MODE Default                       |
### Mode 3 (Temperature)
| Fingers                   | Operation                          |
|---------------------------|------------------------------------|
| 1 to 5 fingers up         | Cycle through temperature levels   |
| Index finger and Pinky up | MODE Default                       |
### Mode 4 (Color)
| Fingers                   | Operation                          |
|---------------------------|------------------------------------|
| 1 to 5 fingers up         | Cycle through set of colors        |
| Index finger and Pinky up | MODE Default                       |
