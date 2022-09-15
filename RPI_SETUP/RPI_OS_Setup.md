# Tutorial of Dietpi setup on a Raspberry PI via wifi #

## Why DietPi? ##
The DietPi is a lightweight Debian-based Linux distribution that can be used as a host operating system on Raspberry Pi devices. 

## Equipment  ##
### Recommended ###
1. Laptop or Desktop - I am using my personal laptop with Windows 11 OS. It is a 11th Gen Intel Core-i7 64-bit operating system.
2. Raspberry Pi - I am using a Raspberry Pi 4 Model B 2019. (Purchase Link: )
3. Micro SD Card (8GB+) - I am using a Lexar 32 GB Micro SD card. (Purchase Link: )
4. Wi-Fi - I am using GL.iNet GL-MT300N-V2 portable travel wireless VPN router. (Purchase Link: )
Checkout the link if you need help in setting up WI-FI router. 

### Optional ###
1. Raspberry Pi Case
2. SD Card Converter/ Card Reader

With all the equipment ready you are good to follow the below steps !!

### Download an extractor and Image flasher on your laptop ###
1. Extractor - We use the extractor to extract the diet-pi image file.
   - For Windows, use BreeZip http:www.breezip.com or 7-Zip https://www.7-zip.org. 
2. balenaEtcher - We use the balena Etcher https://www.balena.io/etcher/ to burn the diet-pi image to sd card. 

### Download and configure  DietPI on your laptop
1. Download and extract the DietPi disk image
   - Go to https://dietpi.com/#download and select the RaspberyPI Images
   - On the new page choose the download for your targeted pi
       - I downloaded: ARMv8 64-bit image: https://dietpi.com/downloads/images/DietPi_RPi-ARMv8-Bullseye.7z  
   - Extract the DietPi_RPi-ARMv8-Bullseye.7z -
2. Write the DietPi image to your SDcard using balenaetcher
   - In the balenaEtcher, Select the dietpi image ( you can drag and drop or from choose file option )
   - Select the targeted card
   - Click on flash
      - Wait until the flashing and validating are done
   - Close balenaetcher
3. Configure the boot image on the microSD card of dietpi.
   - copy dietpi.txt and dietpi-wifi.txt to a temporary directory
   - edit dietpi-wifi.txt with your router SSID and its password.
      
      |Lines to change | Example |
      | ------------- | ------------- |
      |aWIFI_SSID[0]=''  | aWIFI_SSID[0]='VU-FALL22-IOT' |
      |aWIFI_KEY[0]='' |  aWIFI_KEY[0]='123pass' |

   - edit dietpi.txt with your location and wifi network default settings
     |Values for East Coast US settings|
     | ------------- |
      AUTO_SETUP_LOCALE=en_US.UTF-8
      AUTO_SETUP_KEYBOARD_LAYOUT=us
      AUTO_SETUP_TIMEZONE=America/New_York
      AUTO_SETUP_NET_ETHERNET_ENABLED=0
      AUTO_SETUP_NET_WIFI_ENABLED=1
      AUTO_SETUP_NET_WIFI_COUNTRY_CODE=US
      AUTO_SETUP_DHCP_TO_STATIC=1
      AUTO_SETUP_NET_HOSTNAME=DietPi_{YOUR_INITIALS}
      AUTO_SETUP_HEADLESS=1
      AUTO_SETUP_AUTOSTART_TARGET_INDEX=1
      SURVEY_OPTED_IN=0
      CONFIG_SERIAL_CONSOLE_ENABLE=1
   
         - Change {YOUR_INITIALS} with a unique string. For example, I used SSI so it would be DietPi_SSI.
         - Save the changes
4. Copy the dietpi.txt and dietpi-wifi.txt you edited to the top level directory of your sd card.

5. Eject the SD card from your laptop

### Running DietPi in RPI
1. Install SD card onto the PI and powerup the PI.
        - It is adviced to used Raspberry Pi with its case since RPI is fragile and has exposed circuitry that can quickly get damaged
2. Red light turn on and green light starts flashing as the install is running
3. Wait until the green light has finished flashing

### Login to the DietPi

1. Using the admin website of your router at
   - check the CLIENTS page for the IPADDR of the pi that is booted up.
   - use SSH to login into your PI using
   
  |Command| Password|
  | ------------- |-------------|
  | ssh root@IPADDR |       dietpi|
    
   - Now the installations start and the connection will be closed automatically.
   - SSH Login to PI again. This time DietPi interface will be opened prompting you to change the Software and User password. Be sure to change the passwords.
   
### You are now ready to start install platform software.
Follow the tutorial to install IOT platform software [IOT Platform Install](../RPI_IOT_PLATFORM_INSTALL_tutorial)
