- [Home-Assistant](#home-assistant)
  - [Devices - Hardware](#devices---hardware)
  - [Devices - Software](#devices---software)
  - [Screenshots](#screenshots)

# Home-Assistant 

[![Build Status](https://travis-ci.org/huczas/.homeassistant.svg?branch=master)](https://travis-ci.org/huczas/.homeassistant) [![HitCount](http://hits.dwyl.io/huczas/.homeassistant.svg)](http://hits.dwyl.io/huczas/.homeassistant) [![Black Duck Security Risk](https://copilot.blackducksoftware.com/github/repos/huczas/.homeassistant/branches/master/badge-risk.svg)](https://copilot.blackducksoftware.com/github/repos/huczas/.homeassistant/branches/master)

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
* Xiaomi AirPurifier 2S
* Xiaomi Mi Flora - Flower health
* Ikea TRÅDFRI - gateway, and some light bulbs

## Devices - Software

* Raspberry Pi 3B
  * Raspbian - Stretch
  * [Home-assistant] in Python venv
  * [MQTT] - Built in HBMQTT broker
  * [InfluxDB] - latest version
  * [Grafana] - latest version
  * [PiHole] - automated install
  * [SSMTP] - sending emails from RPi
  * [Security] - secure ssh
* Esp8266:
  * [EspEasy]

[Home-assistant]:../master/info/Help.md
[MQTT]:../master/info/MQTT.md
[Grafana]:../master/info/Grafana.md
[InfluxDB]:../master/info/InfluxDB.md
[PiHole]:https://github.com/pi-hole/pi-hole#one-step-automated-install
[SSMTP]:../master/info/email.md
[Security]:../master/info/security.md
[EspEasy]:https://github.com/letscontrolit/ESPEasy

## Screenshots

![Home](../master/info/screenshots/ha_home.png)
![Pogoda](../master/info/screenshots/ha_pogoda.png)
![Settings](../master/info/screenshots/ha_settings.png)
