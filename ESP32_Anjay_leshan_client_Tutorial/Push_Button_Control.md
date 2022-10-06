## ESP32 Anjay leshan client experiments - Push Button control

In this Tutorial, we will see how we can record the push button activites in Leshan server. The button is a basic component and widely used in many ESP32 projects. In the code, by reading the state of the input pin, we can infer the button is pressed or not.

**How Button Works**
- When the button is pressed, the pin A is connected to the pin B
- When the button is NOT pressed, the pin A is NOT connected to the pin B

### Components:

- Push Button
- Raspberry Pi
- ESP32
- 2 220 Ohm pull up resistor
- Breadboard
- 2 Jumper wires

### Wiring 



### Building Anjay Client:

Assuming that anjay-esp32-client directory is setup and your ESP32 is registered in leshan server. 

1. move to the anjay-esp32-client directory
```
cd ~/projects/Anjay-esp32-client
```

2. Setup the local enironment for using the esp tools
```
cd ~/projects/Anjay-esp32-client
. $HOME/esp/esp-idf/export.sh
idf.py set-target esp32 
```
3. setup the device requirements
     ```
     cd ~/projects/Anjay-esp32-client
     idf.py menuconfig
     ```
     - navigate to "Component Config->" 
     - select anjay-esp32-client

     Setup your config to be:
     (anjay-esp32-client) Endpoint name
     (coap://{LESHAN_SERVER_IP}:5683) Server URI
     Choose socket (UDP)  --->
     Choose security mode (Non-secure connection)  --->


     - navigate to "Board - > "

     -  navigate to "Client options ->"
          - Change Server URI from coaps://try-anjay.avsystem.com:5684 to  coaps://YOUR_LESHAN_SERVER_IP_ADDR:5684
	    I used coaps://192.168.8.224:5684
	    Your IP my be different
	    
     -  navigate to "WiFi ->"
         To enter your IOT ROUTER WIFI SSID and key to allow the esp32 acccess to your router and PI.
	 
4. Build the code for the device using
    
    ```
     cd ~/projects/Anjay-esp32-client
     idf.py build
     ```

 
