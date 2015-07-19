#RDM Makerspace access system

##SW

###Set up Raspbian

Burn [latest Rasbian image](https://www.raspberrypi.org/downloads/) on uSD card

Expand rootsystem

Advanced options > Enable I2C

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get dist-upgrade
$ sudo reboot
```

####WiringPi
```
sudo apt-get install git-core
git clone git://git.drogon.net/wiringPi
cd wiringPi
git pull origin
./build

gpio -v
gpio readall
```

####I2C

```
sudo apt-get install i2c-tools
sudo apt-get install python-smbus
sudo adduser pi i2c
sudo reboot
```

Add to /etc/modules
```
i2c-bcm2708
i2c-dev
```

Add to /etc/rc.local
```
modprobe i2c-dev
```

###Enable RTC

Install battery

Check if RTC shows up at 0x6f using
```
i2cdetect -y 1
```

Add to /etc/rc.local
```
modprobe i2c:mcp7941x
echo mcp7941x 0x6f > /sys/class/i2c-dev/i2c-1/device/new-device
```

Reboot

```
sudo date -s "7 MAY 2015 21:27:00"

####Freeing UART

$ sudo raspi-config

From the main menu, select option 7 (Serial), then select 'No' to disable shell and kernel messages via UART.

$ sudo reboot

###Build libnfc

See https://learn.adafruit.com/adafruit-nfc-rfid-on-raspberry-pi/building-libnfc

```