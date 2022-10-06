## Install utils and libraries to build anjay ###

Logon to Raspberry Pi using SSH

Install the utils and libraries in any directory using sudo

``` 
sudo apt-get install git build-essential cmake libmbedtls-dev zlib1g-dev
```

## Build and install the avs_commons system ##

1. clone the avs_commons repo
```
cd ~/projects
git clone https://github.com/AVSystem/avs_commons
```
2. Build and install the avs_commons library
```
cd ~/projects/avs_commons
cmake . && make && sudo make install
```

You have now built and installed the avs_commons library into share directories

## Build and install the ANJAY Library ##

1. retrieve the anjay code
```
cd ~/projects
git clone https://github.com/AVSystem/Anjay
```
2. build the anjay code
```
cd ~/projects/Anjay
git submodule update --init
cmake . -DDTLS_BACKEND="mbedtls"
make -j
```
3. try the anjay demo

-- view the leshan test server at https://leshan.eclipseprojects.io/#/clients
-- run the demo and see your machine listed in the leshsn server
```
./output/bin/demo --endpoint-name $(hostname) --server-uri coap://leshan.eclipseprojects.io:5683
```

### Installing Anjay library objects

```
cd ~/projects/Anjay
cmake -DCMAKE_INSTALL_PREFIX=/home/dietpi/projects/Anjay-esp32-client . && make &&  make install
```


**Note:** If the build does not work then delete the Anjay-esp32-client directory and clone a prebuilt version using:

```
cd projects
git clone --recurse-submodules --remote-submodules https://github.com/pschragger/Anjay-esp32-client
```

