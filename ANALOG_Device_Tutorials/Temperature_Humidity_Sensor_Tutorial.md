# HOW TO SET UP THE DHT11 SENSOR ON THE RASPBERRY PI

## What is DHT11 sensor
The DHT11 temperature and humidity sensor is a little sensor that provides digital temperature and humidity readings. These sensors are popular for use in remote weather stations, soil monitors, and home automation systems.

### Components:

  - DHT11 Temperature and Humidity Sensor(4-pin)
  - Raspberry Pi
  - 10K Ohm pull up resistor
  - Breadboard
  - 3 Jumper wires
 
### Wiring for SSH terminal output
If you have a four pin DHT11 and want to output the humidity and temperature to the SSH terminal, wire it like this:
    - Connect the VCC pin of DHT11 to 2nd pin of Raspberry Pi GPIO
    - Connect the signal pin of DHT11 to 7th pin of Raspberry Pi GPIO
    - Connect the ground pin of DHT11 to 6th pin of Raspberry Pi GPIO
    - The resistor is connected between the VCC and signal lines.
### Programming the DHT11
We’ll be using WiringPi to program the DHT11 in C. If you don’t have WiringPi installed already, install the "WiringPi" from DietPi Software interface. or follow this link for instructions on [how to install WiringPi](https://projects.drogon.net/raspberry-pi/wiringpi/download-and-install/).

After Wiring-Pi is successfully installed, copy the C
