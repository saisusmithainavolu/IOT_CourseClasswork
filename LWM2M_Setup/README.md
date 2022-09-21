## In this directory we will find the tutorial to setup Leshan LWM2M server on RaspBerry Pi and experiments performed on Leshan Server

Follow the tutorial for installation of Leshan LWM2M server on RaspBerry Pi [LWM2M Server Setup](https://github.com/pschragger/IOT_Tutorials_for_VU/blob/main/RPI_DEVICE_MANAGEMENT_INSTALL_tutorial/README.md)

## Additional steps done 

I have additionally installed Java JRE and node.js along with Java JDK, Git to avoid further errors in the process.

1. Install Java JRE
    - On command line in dietpi start dietpi-software
    ```
    sudo dietpi-software
    ```
    - search for node.js 
    - press spacebar to select 
    - tab to ok and press enter
    - navigate to install on dietpi-software menu page
    - press enter and it should show that the software 
    ```
    - Java JRE: OpenJDK Runtime Environment
    ```
    - navagate with tabs to <ok> and press enter
   - install should begin using apt scripts

2. Install node.js
     - On command line in dietpi start dietpi-software
    ```
    sudo dietpi-software
    ```
    - search for node.js 
    - press spacebar to select 
    - tab to ok and press enter
    - navigate to install on dietpi-software menu page
    - press enter and it should show that the software 
    ```
    - Node.js : JavaScript runtime environment
    ```
    - navagate with tabs to <ok> and press enter
    - install should begin using apt scripts
  
## Experiments ##

I ran the bootstrap server, created objects in the dietPi client and used wireshark to analyze the protocols 
