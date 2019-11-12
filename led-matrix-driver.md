# My rPi x LED matrix setup

For controling a matrix of LEDS

## Gear
* RaspberryPi 3B+
* [Henner Zeller Active-3](https://github.com/hzeller/rpi-rgb-led-matrix/tree/master/adapter/active-3) pi-hat, produced by [ACME Systems](https://www.acmesystems.it/HAT-A3)
*  Three chains of five 64x64 LED Matrix units

## Driving the display

Three options:
* Manually issue commands to run scripts with CLI args, via ssh (C++ or Python3 below).
* Run pre-programmed sets of scripts with CLI args from the android app [RaspController](https://play.google.com/store/apps/details?id=it.Ettore.raspcontroller&hl=en_US).
* Start the device in [PixelPusher](http://www.heroicrobotics.com/products/pixelpusher) receiver mode, then send frames created with [Processing](https://processing.org/), [p5.js](https://p5js.org/), or   [Christopher Schardt](http://ledlabs.co/)'s iOS app [L.E.D. Lab](https://apps.apple.com/us/app/l-e-d-lab/id832042156)


### Run as a PixelPusher receiver (daemon)
#### start pixel-push daemon:
sudo /home/pi/rpi-matrix-pixelpusher/pixel-push -u 8192 -i wlan0 --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-daemon

#### kill pixel-push deamon:
sudo kill -9  $(ps -ef | grep /home/pi/rpi-matrix-pixelpusher/pixel-push | grep -v grep | awk '{print $2}')


## Commands

### C++ library demos
#### gif & image viewer:
`sudo ./led-image-viewer ~/images/homer-simpson-relaxing.gif --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-show-refresh`

`sudo /home/pi/rpi-rgb-led-matrix/utils/led-image-viewer ~/images/logo-dark.jpeg --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-show-refresh`
#### scrolling text:
`sudo /home/pi/rpi-rgb-led-matrix/examples-api-use/scrolling-text-example -f ../fonts/10x20.bdf hey --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-show-refresh`
#### rotating block:
`sudo /home/pi/rpi-rgb-led-matrix/examples-api-use/demo --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-show-refresh -D 0`
#### scrolling image: ####
`sudo /home/pi/rpi-rgb-led-matrix/examples-api-use/demo --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-show-refresh -D 1 runtext.ppm`

### Python3 library demos
#### show image:
`sudo python3 /home/pi/rpi-rgb-led-matrix/bindings/python/samples/image-viewer.py ~/images/logo-dark.jpeg --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-show-refresh`
#### rotating block:
`sudo python3 ./rotating-block-generator.py --led-gpio-mapping=regular --led-chain=5 --led-cols=64 --led-rows=64 --led-parallel=3 --led-show-refresh`
