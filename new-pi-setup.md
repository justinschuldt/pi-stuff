### update packages
* `sudo apt-get update -y`
* `sudo apt-get upgrade -y`

### software settings
`sudo raspi-config`
* update localization
* change password
* set hostname
* connect to wifi
* enable ssh
* optionally: enable SPI, I2C
* unpack storage

### general software to install
`sudo apt-get install -y git`

### for passwordless ssh access,  copy ssh key to device:
`ssh-copy-id <USERNAME>@<IP-ADDRESS>`

### for LED matrix pHats
to disable sound:

`sudo apt-get install initramfs-tools`

```shell
cat <<EOF | sudo tee /etc/modprobe.d/blacklist-rgb-matrix.conf
blacklist snd_bcm2835
EOF
```

`sudo update-initramfs -u`

### networking

highest priority available network is used

`/etc/wpa_supplicant/wpa_supplicant.conf`

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
	ssid="network-one"
	psk="secret-one"
	priority=3
}
network={
	ssid="network-two"
	psk="secret-two"
	priority=4
}
```

### mount nfs volume on boot

add to `/etc/fstab`:
```
192.168.86.29:/volume1/video /home/pi/videos nfs rw,auto,hard,intr 0 0

```
note: ensure the `sudo raspi-config` Boot Option (3): Wait for Network at Boot (B2) is enabled
