# Home-Assistant help

## HASS operations

* To check realtime logs `sudo journalctl -f -u home-assistant.service`
* To restart HA `sudo systemctl restart home-assistant.service`
* To check logs `sudo systemctl status -l home-assistant.service`
* To stop HA `sudo systemctl stop home-assistant.service`
* To start HA `sudo systemctl start home-assistant.service`

## To upgrade HASS manually

1. Login to system. HASS configuration files are saved in `/home/homeassistant/.homeassistant` and the code files are saved in `/srv/homeassistant/homeassistant_venv/lib/python3.6/site-packages/homeassistant`.
2. Change to homeassistant user `sudo su -s /bin/bash homeassistant`
3. Change to virtual enviroment `source /srv/homeassistant/homeassistant_venv/bin/activate`
4. Update HA `pip3 install --upgrade homeassistant`. To update to a different branch, use the complete git URL, `pip3 install --upgrade git+git://github.com/home-assistant/home-assistant.git@dev`. To install specific version of HA use `pip3 install homeassistant==0.XX.X`.
5. Type `exit` to logout the hass user and return to the `pi` user.
6. Restart the Home-Assistant Service `sudo systemctl restart hhome-assistant.service`

## If RPi is not syncing the time

Use the `systemd-timesyncd` service as explained [here](https://wiki.archlinux.org/index.php/systemd-timesyncd)
Here are the [time servers](https://wiki.archlinux.org/index.php/Network_Time_Protocol_daemon#Connection_to_NTP_servers) that I used.

```BASH
NTP=0.pl.pool.ntp.org 1.pl.pool.ntp.org 2.pl.pool.ntp.org 3.pl.pool.ntp.org
FallbackNTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
```

## Configuring WinSCP to edit HASS files

Default AIO installation does not allow editing the configuration files in WinSCP. To enable the same, you will need to change the SFTP server (in Advanced settings -> Environment -> SFTP).

1. Obtain the SFTP by running `grep sftp /etc/ssh/sshd_config` at the `pi` shell. You will get something like, `Subsystem sftp /usr/lib/openssh/sftp-server`.
2. Now, set the sftp server to: `sudo su -c /usr/lib/openssh/sftp-server` (note that the `/usr/lib/openssh/sftp-server` is the same path obtained from the previous step) and set Shell to `sudo -s`.

## Mosquitto operations

I am using the default AIO username/password, replace them with yours

1. You can remove a topic from Mosquitto using `mosquitto_pub -r -n -u 'pi' -P 'raspberry' -t 'owntracks/arsaboo/mqttrpi'`
2. To subscribe to all the topics use `mosquitto_sub -h 192.168.2.212 -u 'pi' -P 'raspberry' -v -t '#'` (replace the IP address)
3. To publish use `mosquitto_pub -u 'pi' -P 'raspberry' -t 'smartthings/Driveway/switch'  -m 'on'` (use the relevant topic).
4. You can find the path to mosquitto_pub using `which mosquitto_pub`; restart Mosquitto using `sudo systemctl restart mosquitto`.

## Backing up Configurations on Github

Thanks to @dale3h for assistance with these instructions.

1. Install `git` using `sudo apt-get install git`
2. Go to <https://github.com/new> and create a new repository. I named mine `homeassistant-config`. Initialize with `readme: no` and `.gitignore: none`.
3. Navigate to your `.homeassistant` directory. For AIO, it should be `/home/homeassistant/.homeassistant`, and for HASSbian, it is `/home/hass/.homeassistant`.
4. Run `sudo su -s /bin/bash homeassistant` for AIO and `sudo su -s /bin/bash hass` for HASSbian.
5. Run `wget https://raw.githubusercontent.com/arsaboo/homeassistant-config/master/.gitignore` to get the `.gitignore` file from your repo (replace the link to match your repository). You can add things to your `.gitignore` file that you do not want to be uploaded.
6. Next, we need to add SSH keys to your Github account.
    * Navigate to `cd /home/homeassistant/.ssh` (for AIO). If you don't have `.ssh` directory, create one and change the permission `chmod 700 ~/.ssh`.
    * Run `ssh-keygen -t rsa -b 4096 -C "homeassistant@pi"`. If you want to enter a passphrase, that's up to you. If you do, you'll have to enter that passphrase any time you want to update your changes to github. If you do not want a passphrase, leave it blank and just hit `Enter`.
    * Save the key in the default location (press `Enter` when it prompts for location).
    * When you're finished, run `ls -al ~/.ssh` to confirm that you have both `id_rsa` and `id_rsa.pub` files.
    * Go to <https://github.com/settings/keys> and click `New SSH key` button at top right. Title: `homeassistant@pi` (or whatever you want, really...it's just for you to know which key it is)
    * Run `cat id_rsa.pub` in the SSH session and copy/paste the output to that github page.
    * Then click `Add SSH key` button and provide your github password.
7. Go back to your repo page on GitHub. It'll be something like <https://github.com/yourusernamehere/.homeassistant.> Click the green `Clone or download` button, and then click `Use SSH`.
8. You should see something like this in the textbox: `git@github.com:yourusername/.homeassistant.git`. Copy that to your clipboard.
9. Now you are ready to upload the files to GitHub.
    * Navigate to `cd ~/.homeassistant`
    * `git init`
    * `git add .`
    * `git commit -m 'initial commit'`
    * If you get an error about `*** Please tell me who you are.`, run `git config --global user.email "your@email.here"` and `git config --global user.name "Your Name"`
    * After that commit succeeds, run: `git remote add origin git@github.com:yourusername/.homeassistant.git` (make sure you enter the correct repo URL here)
    * Just to confirm everything is right, run `git remote -v` and you should see:
      ```bash
      hass@raspberrypi:~/.homeassistant$ git remote -v
      origin  git@github.com:huczas/homeassistant-config.git (fetch)
      origin  git@github.com:huczas/homeassistant-config.git (push)
      ```
    * Finally, run `git push origin master`.

10. For subsequent updates:
    * `cd /home/homeassistant/.homeassistant`
    * `sudo su -s /bin/bash homeassistant`
    * `git add .`
    * `git commit -m 'your commit message'`
    * `git push origin master`
11. To restore from your Github repository (replace the URL):
    ```bash
    sudo su -s /bin/bash homeassistant
    cd /home/homeassistant
    git clone git@github.com:huczas/.homeassistant.git .homeassistant
    ```

## Integrating HASS (AIO) with Smartthings using Mosquitto

If you are using AIO (which has Mosquitto pre-installed), you can use the following to integrate SmartThings and HA.

1. Install node.js, and pm2
    ```bash
    sudo apt-get update && sudo apt-get upgrade -y
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs
    sudo npm install -g pm2
    sudo su -c "env PATH=$PATH:/usr/local/bin pm2 startup systemd -u pi --hp /user/pi"
    ```
2. Install the [SmartThings MQTT Bridge](https://github.com/stjohnjohnson/smartthings-mqtt-bridge)
    ```bash
    sudo npm install -g smartthings-mqtt-bridge
    ```
3. Add details of your Mosquitto to `config.yml`. For the default AIO username password, your file should look something like:
    ```text
    mqtt:
        # Specify your MQTT Broker's hostname or IP address here
        host: mqtt://192.168.2.199
        # Preface for the topics $PREFACE/$DEVICE_NAME/$PROPERTY
        preface: smartthings

        # Suffix for the state topics $PREFACE/$DEVICE_NAME/$PROPERTY/$STATE_SUFFIX
        # state_suffix: state
        # Suffix for the command topics $PREFACE/$DEVICE_NAME/$PROPERTY/$COMMAND_SUFFIX
        # command_suffix: cmd

        # Other optional settings from https://www.npmjs.com/package/mqtt#mqttclientstreambuilder-options
        username: pi
        password: raspberry

    # Port number to listen on
    port: 8080
    ```
4. Start ST-MQTT bridge `pm2 start smartthings-mqtt-bridge`
5. Follow the rest of the instructions (from step 2) listed [here](https://github.com/stjohnjohnson/smartthings-mqtt-bridge#usage).
6. Once `pm2` runs the program, you can then run `pm2 save` to save the running programs into a configuration file.
7. You can then run `pm2` as a systemd or service by running the command that you get after running `pm2 startup systemd` (run this without `sudo`).

## Miscellaneous Tips/Tricks

* You can test the Read Speed of your SD card using (note, this command takes some time to run):

  ```bash
  sudo dd if=/dev/mmcblk0 of=/dev/null bs=8M count=100
  sudo hdparm -t /dev/mmcblk0
  ```

* Many of the problems with Pi are related to faulty power supply. You can use `vcgencmd get_throttled` to check if your Pi is getting adequate power supply. You want that to return `throttled=0x0`. If not it means that the Raspberry is throttling itself due to low voltage, or other factors.
* Test Write speed (will create 200MB file in /home/pi/testfile) using `dd if=/dev/zero of=/home/pi/testfile bs=8M count=25`
* To check which files are using up all the space on your SD card, run `sudo du | sort -n`. You can delete the culprits using something like `sudo rm -rf ./.pm2/logs/` (will recursively delete folder /logs/).
