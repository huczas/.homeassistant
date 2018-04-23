<h1 align="center"> Home-Assistant </h1>

<p align="center"><img src="https://github.com/home-assistant/home-assistant-assets/raw/master/loading-screen.gif" width="200"></p>

## Devices - Hardware

* Raspberry Pi 3B
  * BMP680 - gas, pressure, hummidity, temperature
* Esp8266-01
  * BMP280 - hummidity, pressure, temperature
  * BH1750 - Light intensity sensor
* Esp8266-NodeMCU
  * PMS7003 - dust sensor
* Sonoff relay-switch witch ESPEasy software
* Xiaomi Roborock 2 - vacuum
* Xiaomi Mi Flora - Flower health

## Devices - Software

* Raspberry Pi 3B
  * [Raspbian] - Stretch
  * [Home-assistant] in Python venv
  * [MQTT] - Mosquitto
  * [InfluxDB]
  * [Grafana]
  * [PiHole] - automated install
  * [SSMTP] - sending emails from RPi
* Esp8266:
  * [EspEasy]

[Raspbian]:https://www.raspberrypi.org/downloads/raspbian/
[Home-assistant]:../master/info/Help.md
[MQTT]:../master/info/MQTT.md
[Grafana]:../master/info/Grafana.md
[InfluxDB]:../master/info/InfluxDB.md
[PiHole]:https://github.com/pi-hole/pi-hole#one-step-automated-install
[SSMTP]:../master/info/email.md
[EspEasy]:https://github.com/letscontrolit/ESPEasy

## Screenshots

![Home](../master/info/screenshots/ha_home.png)
![Pogoda](../master/info/screenshots/ha_pogoda.png)
![Settings](../master/info/screenshots/ha_settings.png)
