# Stuffly
Stuffly is an IoT app built during the Andela IoT Hackathon. It basically gives real time updates on temperature, humidity and air-pressure for a particular room. Through this, we can determine if a room is stuffy or not &mdash; hence the name **stuff**ly.

We've currently built a client Slack bot for Andela Slack Org, called _@stuffly_ through which you can interact with the IoT app.

## Schematic Diagram

Simple digram explaining our setup:

![stuffly-dgm-01](https://cloud.githubusercontent.com/assets/13568167/17643990/5cee937c-6183-11e6-8523-45bae93f9180.png)

## Setting Up Arduino

Download and install Arduino IDE for mac [here](https://www.arduino.cc/en/Main/Software).
This adds an Arduino directory (referred to as a sketchbook) into your Documents folder.
Go into libraries folder and clone the BME280 libraries

## Setting up BM8 libraries

Clone the BME280 repositories to your the sketchbook libraries directory.

```bash
cd Arduino/libraries

git clone git@github.com:adafruit/Adafruit_BME280_Library.git

git clone git@github.com:adafruit/Adafruit_Sensor.git
```

## Wiring Setup

The components required are as follows:
* Breadboard
* Arduino Microcontroller
* BME 280 Humidity Barometric Pressure Temperature Sensor Breakout
* Jumper cables
* Arduino to USB cable
* External DC Power Supply (for portability)

### Connect the components together as follows:

* Connect Vin to the power supply, 3-5V is fine. Use the same voltage that the microcontroller logic is based off of. For most Arduinos, that is 5V.
* Connect GND to common power/data ground.
* Connect the SCL pin to the I2C clock SCL pin on your Arduino. On an UNO & '328 based Arduino, this is also known as A5, on a Mega it is also known as digital 21 and on a Leonardo/Micro, digital 3.
* Connect the SDA pin to the I2C data SDA pin on your Arduino. On an UNO & '328 based Arduino, this is also known as A4, on a Mega it is also known as digital 20 and on a Leonardo/Micro, digital 2.


This is shown below:

![here] (/stuffly_breadboard.jpg)


## Connect the board

The Arduino Uno, and Mega automatically draw power from either the USB connection to the computer or an external power supply. The power source is selected with a jumper, a small piece of plastic that fits onto two of the three pins between the USB and power jacks. Check that it's on the two pins closest to the USB port.

Connect the Arduino board to your computer using the USB cable. The green power LED (labelled PWR) should go on.

## Select the board
You'll need to select the entry in the Tools > Board menu that corresponds to your Arduino.

## Select your Serial Port

Select the serial device of the Arduino board from the Tools > Serial Port menu. On the Mac, this should be something with /dev/tty.usbmodem (for the Uno or Mega 2560) or /dev/tty.usbserial (for older boards) in it.

## Clone the Stuffly repo

Run this to clone the stuffly repo

```bash
git clone https://github.com/andela-anandaa/stuffly.git
```

Make the `read_arduino.sh` bash file executable
```bash
chmod u+x stuffly/arduino/read_arduino.sh
```

## Upload the sensor to the arduino board
Open `stuffly/arduino/arduino.ino` on the arduino IDE and click upload to push it on to the board.

Run `./read_arduino.sh` to read the temperature, humidity, air pressure levels to an sqlite database.


# Slack Bot

## Usage
You can send the following messages to @stuffly bot to get the states of various rooms:

- Is [room] stuffy?
- What is the temperature at [room]?
- What is the humidity at [room]?



## Dev
We are using the [slackbot](https://github.com/lins05/slackbot) Python package.

`slackbot_settings.py` is excluded because of obscuring the `API_TOKEN`. However, this is the format:

```
API_TOKEN = "xoxb-xxxxxxxx"

PLUGINS = [
    'slackbot.plugins',
    'mybot.plugins'
]
```

To run the Slack bot:
```
$ cd stuffly
$ python -m bot.bot
```

## Quick Note on Firebase
- We're using the [python-firebase](https://pypi.python.org/pypi/python-firebase/1.2) package.
- `_firebase/config.py` file is gitignored but this is the format of the content:
```python
config = {
    "firebase": "https://<your-firebase-url>.firebaseio.com/"
}
```
- NB: should migrate to using [pyfirebase](https://github.com/andela-cnnadi/pyfirebase), which is much cleaner.

# Credits
Big shout-out to the _HackHeads_ team:

- [@andela-emabishi](https://github.com/andela-emabishi) (Team Lead)
- [@johnkariuki](https://github.com/johnkariuki)
- [@bernard-kanyolo](https://github.com/bernard-kanyolo)
- [@andela-omugeri](https://github.com/andela-omugeri)
- [@andela-anandaa](https://github.com/andela-anandaa)
