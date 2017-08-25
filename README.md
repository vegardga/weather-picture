# weather-picture
Picture that fetches weather data and light up LEDs based on it.

## Picture
![Weather picture](https://github.com/vegardga/weather-picture/blob/master/images/picture.png "Weather picture")

Icons designed by [Freepik](https://www.flaticon.com/authors/freepik) from Flaticon.

Quote taken from MagPi issue [#57](https://www.raspberrypi.org/magpi/issues/57/).

QR code generated with [QR Code Generator](http://goqr.me/).

## Code
```python
try:
    import urllib.request as urllib2
except ImportError:
    import urllib2
import json
import sys
from gpiozero import LED
from time import sleep

rainled = LED(17)
sunled = LED(18)
snowled = LED(27)
windyled = LED(22)

def toggleLed(led, val):
  if val > 0:
    led.on()
  else:
    led.off()
  sleep(1)

def checkWeather():
  try:
    content = urllib2.urlopen('http://vegardga.no/api/weather/json').read()
    weather = json.loads(content.decode())
    toggleLed(rainled, weather['rain'])
    toggleLed(snowled, weather['snow'])
    toggleLed(sunled, weather['sun'])
    toggleLed(windyled, weather['windy'])
  except:
    e = sys.exc_info()[0]
    print("Error - ", e)

while True:
  checkWeather()
  sleep(10)
```

## Crontab
```bash
@reboot python3 /home/pi/weather.py &
```

## Final
![With lights](https://github.com/vegardga/weather-picture/blob/master/images/IMG_8022.JPG "With lights")

![Raspberry Pi Zero W](https://github.com/vegardga/weather-picture/blob/master/images/IMG_8018.JPG "Raspberry Pi Zero W")

![From the side](https://github.com/vegardga/weather-picture/blob/master/images/IMG_8019.JPG "From the side")

![Quote](https://github.com/vegardga/weather-picture/blob/master/images/IMG_8026.JPG "Quote")

![Print](https://github.com/vegardga/weather-picture/blob/master/images/IMG_8027.JPG "Print")
