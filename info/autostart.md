# Autostart using systemd

## PYTHON VIRTUAL ENVIRONMENT

If you’ve setup Home Assistant in `virtualenv` following Python installation guide or manual installation guide for Raspberry Pi, the following template should work for you. If Home Assistant install is not located at `/srv/homeassistant`, please modify the `ExecStart=` line appropriately.

```Bash
[Unit]
Description=Home Assistant
After=network-online.target

[Service]
Type=simple
User=%i
ExecStart=/srv/homeassistant/bin/hass -c "/home/homeassistant/.homeassistant"

[Install]
WantedBy=multi-user.target
```

## NEXT STEPS

You need to reload systemd to make the daemon aware of the new configuration.

`$ sudo systemctl --system daemon-reload`
To have Home Assistant start automatically at boot, enable the service.

`$ sudo systemctl enable home-assistant@[your user]`
To disable the automatic start, use this command.

`$ sudo systemctl disable home-assistant@[your user]`
To start Home Assistant now, use this command.

`$ sudo systemctl start home-assistant@[your user]`
You can also substitute the start above with stop to stop Home Assistant, restart to restart Home Assistant, and ‘status’ to see a brief status report as seen below.

```Bash
$ sudo systemctl status home-assistant@[your user]
● home-assistant@fab.service - Home Assistant for [your user]
   Loaded: loaded (/etc/systemd/system/home-assistant@[your user].service; enabled; vendor preset: disabled)
   Active: active (running) since Sat 2016-03-26 12:26:06 CET; 13min ago
 Main PID: 30422 (hass)
   CGroup: /system.slice/system-home\x2dassistant.slice/home-assistant@[your user].service
           ├─30422 /usr/bin/python3 /usr/bin/hass
           └─30426 /usr/bin/python3 /usr/bin/hass
[...]
```