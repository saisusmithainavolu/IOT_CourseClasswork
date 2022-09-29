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

After Wiring-Pi is successfully installed, build the C code using nano and save it with ".c" extension eg: `example.c`
The following C program I used which will output the humidity and temperature (in °C and °F) readings to an SSH terminal
```
#include <wiringPi.h>
#include <stdio.h>
#include <stdlib.h>
#include <stdint.h>
#define MAXTIMINGS	85
#define DHTPIN		7
int dht11_dat[5] = { 0, 0, 0, 0, 0 };
 
void read_dht11_dat()
{
	uint8_t laststate	= HIGH;
	uint8_t counter		= 0;
	uint8_t j		= 0, i;
	float	f; 
 
	dht11_dat[0] = dht11_dat[1] = dht11_dat[2] = dht11_dat[3] = dht11_dat[4] = 0;
 
	pinMode( DHTPIN, OUTPUT );
	digitalWrite( DHTPIN, LOW );
	delay( 18 );
	digitalWrite( DHTPIN, HIGH );
	delayMicroseconds( 40 );
	pinMode( DHTPIN, INPUT );
 
	for ( i = 0; i < MAXTIMINGS; i++ )
	{
		counter = 0;
		while ( digitalRead( DHTPIN ) == laststate )
		{
			counter++;
			delayMicroseconds( 1 );
			if ( counter == 255 )
			{
				break;
			}
		}
		laststate = digitalRead( DHTPIN );
 
		if ( counter == 255 )
			break;
 
		if ( (i >= 4) && (i % 2 == 0) )
		{
			dht11_dat[j / 8] <<= 1;
			if ( counter > 50 )
				dht11_dat[j / 8] |= 1;
			j++;
		}
	}
 
	if ( (j >= 40) &&
	     (dht11_dat[4] == ( (dht11_dat[0] + dht11_dat[1] + dht11_dat[2] + dht11_dat[3]) & 0xFF) ) )
	{
		f = dht11_dat[2] * 9. / 5. + 32;
		printf( "Humidity = %d.%d %% Temperature = %d.%d C (%.1f F)\n",
			dht11_dat[0], dht11_dat[1], dht11_dat[2], dht11_dat[3], f );
	}else  {
	//	printf( "Data not good, skip\n" );
	}
}
 
int main( void )
{
	printf( "Raspberry Pi wiringPi DHT11 Temperature test program\n" );
 
	if ( wiringPiSetup() == -1 )
		exit( 1 );
 
	while ( 1 )
	{
		read_dht11_dat();
		delay( 1000 ); 
	}
 
	return(0);
}
```
Compile the c code using below command
```
gcc -o example example.c -lwiringPi -lwiringPiDev
```

Then run the program with:
```
sudo ./example
```
