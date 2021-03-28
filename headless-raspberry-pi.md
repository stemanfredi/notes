# Headless Raspberry Pi

## Flash the image

Download the Raspberry Pi OS Lite image from https://www.raspberrypi.org/software/operating-systems/.

Flash the image:

    sudo dd bs=4M if=2021-01-11-raspios-buster-armhf-lite.img of=/dev/sdX conv=fsync

## Wireless networking

Add the file `wpa_passphrase.conf` to the microSD boot partition:

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=<Insert 2 letter ISO 3166-1 country code here>

    network={
            ssid="<Name of your wireless LAN>"
            psk="<Password for your wireless LAN>"
    }

The `network` part can be obtained with the command: `wpa_passphrase <ssid>`.

## Remote access

Add an empty file `ssh` to the microSD boot partition.

## First boot

Copy the client ssh public key to the Raspberry

    ssh-copy-id pi@raspberry

Connect

    ssh pi@raspberry

Configure

    sudo raspi-config

Set:

- password
- hostname (optional)
- locale
- timezone

Update Raspbian

    sudo apt update && sudo apt upgrade -y

## References

- https://www.raspberrypi.org/documentation/installation/installing-images/linux.md
- https://www.raspberrypi.org/documentation/configuration/wireless/headless.md
- https://www.raspberrypi.org/documentation/remote-access/ssh/
