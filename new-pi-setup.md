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
