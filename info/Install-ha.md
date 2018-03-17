# Update the system

```Bash
$ sudo apt-get update
$ sudo apt-get upgrade -y
```

Install the dependencies.

`$ sudo apt-get install python3 python3-venv python3-pip`

Add an account for Home Assistant called homeassistant. Since this account is only for running Home Assistant the extra arguments of -rm is added to create a system account and create a home directory.

`$ sudo useradd -rm homeassistant`

Next we will create a directory for the installation of Home Assistant and change the owner to the homeassistant account.

```Bash
$ cd /srv
$ sudo mkdir homeassistant
$ sudo chown homeassistant:homeassistant homeassistant
```

Next up is to create and change to a virtual environment for Home Assistant. This will be done as the homeassistant account.

```Bash
$ sudo su -s /bin/bash homeassistant
$ cd /srv/homeassistant
$ python3 -m venv .
$ source bin/activate
```

Once you have activated the virtual environment (notice the prompt change) you will need to run the following command to install a required python package.

`(homeassistant) homeassistant@raspberrypi:/srv/homeassistant $ python3 -m pip install wheel`
Once you have installed the required python package it is now time to install Home Assistant!

`(homeassistant) homeassistant@raspberrypi:/srv/homeassistant $ pip3 install homeassistant`
Start Home Assistant for the first time. This will complete the installation, create the .homeassistant configuration directory in the /home/homeassistant directory and install any basic dependencies.

`(homeassistant) $ hass`
You can now reach your installation on your Raspberry Pi over the web interface on http://ipaddress:8123.

When you run the hass command for the first time, it will download, install and cache the necessary libraries/dependencies. This procedure may take anywhere between 5 to 10 minutes. During that time, you may get “site cannot be reached” error when accessing the web interface. This will only happen for the first time, and subsequent restarts will be much faster.
