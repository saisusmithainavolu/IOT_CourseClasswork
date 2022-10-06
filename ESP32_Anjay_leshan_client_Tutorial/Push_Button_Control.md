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



### Steps to build/configure Anjay client:

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
     - navigate to **Component Config**
     - select **anjay-esp32-client**
     - navigate to **Board** and setup as below 
     - navigate to **Client options** and setup as below    
     	- Endpoint name --> <client name>  - in my case it is "sinavolu"
     	- Server URI --> coap://{RaspberriPi_IP}:5683 
     	- Choose socket --> UDP 
     	- Choose security mode --> Non-secure connection
     -  navigate to **Connection configuration**
         - enter your IOT ROUTER WIFI SSID and key to allow the esp32 acccess to your router and PI.
     - After all the changes are set, press 'S' to save and 'Q' to quit the menuconfig 
4. Build the code for the push button using
    
    ```
     idf.py build
     ```
5. find the port by using

   ```
   ls -l /dev/ttyUSB*
   ```

6. flash the device  
     ```
     sudo chmod 666 /dev/ttyUSB0
     idf.py -p 0 flash
     ```
     You should see flashing
 
Now you can see the push button object enabled in your ESP32 client in leshan server. You can read the digital input state(False if LED is not turned on and vice versa) and digital input counter(No.of times the button pushed) of the push button. Check out the below video to see the interactions of push button with leshan server
     
 
