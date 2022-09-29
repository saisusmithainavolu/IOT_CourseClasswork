## HOW TO SET UP THE DHT11 SENSOR ON ESP32 WROVER USING ARDUINO IDE

In this Tutorial, we will use the ESP32 to read temperature and humidity data of the DHT11.

### Components:

- DHT11 Temperature and Humidity Sensor(4-pin)
- ESP32 Wrover
- GPIO Extension Board
- 10K Ohm pull up resistor
- Breadboard
- 4 Jumper M/M wires

### Wiring for Arduino terminal
If you have a four pin DHT11 and want to output the humidity and temperature to Arduino, wire it like this:



Connect the ESP32 board to your laptop with the USB cable

### Setting up Ardino IDE

1. Download and install the Arduino IDE from [Arduino Download](https://www.arduino.cc/en/software)
2. Go to File -> Preferences 
    - Add the url to the Additional boards manager Urls https://dl.espressif.com/dl/package_esp32_index.json
3. Go to Tools -> Board -> Boards Manager
    - Search for esp32 and install the “ESP32 by Espressif Systems”
4. Go to Tools -> Board -> esp32 -> ESP32 Wrover Module
    - Select the relevant board
5. Go to Tools -> Port
    - Select the relevant port.(COM3/COM4)
6. Go to Sketch -> Include Library -> Add .ZIP Library…. Select the .zip file from your computer
    -We use the third party library DHTesp. Download the Zip file of the external library from: https://github.com/beegee-tokyo/DHTesp

### Programming the DHT11 in Arduino IDE

Build the C code and save it with ".ino" extension

```
#include "DHTesp.h"
DHTesp dht; //Define the DHT object
int dhtPin = 13;//Define the dht pin
void setup() {
dht.setup(dhtPin, DHTesp::DHT11);//Initialize the dht pin and dht object
Serial.begin(115200); //Set the baud rate to 115200
}
void loop() {
flag:TempAndHumidity newValues = dht.getTempAndHumidity();//Get the Temperature and humidity
if (dht.getStatus() ! = 0) { //Judge if the correct value is
read
goto flag; //If there is an error, go back to
the flag and re-read the data
}
Serial.println(" Temperature:" + String(newValues.temperature) +
" Humidity:" + String(newValues.humidity));
delay(2000);
}
```

-Press the Upload button at the top in Arduino IDE. This will let the code compile and upload to your board.
-Go to the Serial monitor and set the baud rate as "115200".
-You can see the temperature and humidity readings in the Serial Monitor.
