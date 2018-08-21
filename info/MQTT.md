- [MQTT](#mqtt)
    - [MQTT debug](#mqtt-debug)

# MQTT

I'm using from now builtin MQTT Broker with Home-Assistant
More info on that: <https://www.home-assistant.io/docs/mqtt/broker#embedded-broker>

## MQTT debug

To show all topics that are sended to our broker set up on raspberry:

`mosquitto_sub -v -V mqttv311 -t "#"`