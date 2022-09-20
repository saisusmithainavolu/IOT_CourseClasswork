# LWM2M Setup Tutorial #

Leshan is an open source OMA Lightweight Machine to Machine (LWM2M) java client and server implementation. Below are the steps that help you to setup LWM2M on your Raspberry Pi.

## Requirement ##
1. Laptop or Desktop - I am using my personal laptop with Windows 11 OS. It is a 11th Gen Intel Core-i7 64-bit operating system.
2. Raspberry Pi with MicroSD card and DietPi Installed on it. [RPI_OS_Setup](../RPI_SETUP/RPI_OS_Setup.md)
3. Wi-Fi Connectivity. [Router Setup Tutorial](../Setup_Router_Tutorial)

## LWM2M server/client code ##

LWM2M server/client code is available from [eclipse leshan project](https://www.eclipse.org/leshan/) at [ Leshan Github ](https://github.com/eclipse/leshan). In the below steps you will clone the leshan repo to install leshan

## Let's get Started ##

### Install Diet-Pi Software ###
1. Login to Raspberry Pi
```
ssh dietpi@(IPADDR)
```
2. Open the Diet-Pi interface using below command
```
sudo dietpi-software
```
3. Install git
   - 
    - Go to Search Software tab
    - search for git ( should be package 17 )
    - press spacebar to select
    - tab to ok and press enter
    - navigate to install on dietpi-software menu page
    - press enter and it should show that the software 
    ```
    - Git: Clone and manage Git repositories locally
    ```
    - navagate with tabs to <ok> and press enter
    - install should begin using apt scripts
    - check that is installed by using the command on the pi
    ```
    git --version
    ```
2. Install java jdk
      - On command line in dietpi start dietpi-software
    ```
    sudo dietpi-software
    ```
    - search for Java JDK ( should be package 8 )
    - press spacebar to select 
    - tab to ok and press enter
    - navigate to install on dietpi-software menu page
    - press enter and it should show that the software 
    ```
    - Java JDK: OpenJDK Development Kit
    ```
    - navagate with tabs to <ok> and press enter
    - install should begin using apt scripts
    - check that is installed by using the command on the pi
    ```
    java --version
    ```
2. Install node.js
     - On command line in dietpi start dietpi-software
    ```
    sudo dietpi-software
    ```
    - search for node.js 
    - press spacebar to select 
    - tab to ok and press enter
    - navigate to install on dietpi-software menu page
    - navagate with tabs to <ok> and press enter
   - install should begin using apt scripts
3. Install maven
   1. In the dietpi command prompt, create a download directory
   ```
   mkdir download
   ```
   2. change directory into the download directory
   ```
   cd download
   ```
   3. download the latest maven tarball using wget, the following is an example - be sure to check the latest version on [apache maven site](https://maven.apache.org/download.cgi)  
   ```
   wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz
   ```
   4. unpack the tarball
   ```
   tar xzvf apache-maven-3.8.6-bin.tar.gz
   ```
   5. Add the bin directory of the created directory apache-maven-3.8.6 to the PATH environment variable
   6. Confirm installation using
   ```
   mvn -v
   ```
   7. Setup the environment variables to add maven to the paths taken from [maven install instructions](https://maven.apache.org/install.html)
      - add the bin directory to the path
      ```
      echo 'PATH="${PATH}:~/download/apache-maven-3.8.6/bin"' >>  ~/.bashrc
      ```
   8.  test maven installation using
   ```
   bash
   mvn -v
   ```
  
image
   
   9. create a JAVA_HOME environment variable

      - add the JAVA_HOME to the .bashrc
      ```
      sudo echo 'JAVA_HOME="/usr/lib/jvm/java-17-openjdk-arm64"' >> ~/.bashrc
      ```
      - check that the install was complete with
      ```
      bash
      echo $JAVA_HOME
      ```
image

4. Install leshan git and build form [leshan git](https://github.com/eclipse/leshan)
   - clone the leshan repo using
   
image
   
   cloning the directory should be less than a minute
   - build leshan
   
image
   


### Test the leshan server
1. Start the server using
  ```
  cd ~/projects/leshan
  java -jar leshan-server-demo/target/leshan-server-demo-*-SNAPSHOT-jar-with-dependencies.jar &
  ```
  -  Connect on Leshan demo UI: http://RPI_IPADDR:8080

   My Raspberry PI is using 192.168.8.224 ( from the router admin client page)
   therefore I will use
   ```
   http://192.168.8.224:8080
   ```
   this will bring up te leshan register client page


  - run the leshan client to add it to the page
  ```
  java -jar leshan-client-demo/target/leshan-client-demo-*-SNAPSHOT-jar-with-dependencies.jar
  ```

  The result should show the registration of your DietPI host as a Temperature client endipoint
  This end point should continue to register every minute.
  using ctrl-c to stop the client

  ### check the server page in the leshan server page to see the active url info and public keys and server cert info

###  Continue to the ESP32 lwm2m client build ###

