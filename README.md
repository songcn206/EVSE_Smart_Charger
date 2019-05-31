# EVSE Smart Charger

By: Andy Begey, Brandon Metcalf, Luis Contreras, Shermaine Dayot, Omair Farooqui, Krishan Solanki, Alex Ramirez, Emon Sahaba

Project Managers: Dr. Michael Klopfer, Prof. GP Li. 

University of California, Irvine - California Institute for Telecommunications and Information Technology (Calit2)  

---
Example ESP32-WROOM-32 application demo: operation of Electric Vehicle Supply Equipment (EVSE) Smart Charger that connects to the internet and MQTT server which will allow EV owners to control the charging schedules and monitor power consumption. Uses Smartenit MQTT format. 

Example Application note for ESP32-WROOM-32

Copyright © The Regents of the Univeristy of California, 2018-19

Released into the public domain.

# Installation
Required tasks needed for the project: 

1. Install Arduino ESP32 on Windows using this link: https://github.com/espressif/arduino-esp32/blob/master/docs/arduino-ide/windows.md

2. Open Arduino IDE. Click File->Open, then navigate to the following path:    
`EVSE code/Arduino/Current_Year_DevelopmentFirmware/EVChargerESP32RTOS`

3. Open `EVChargerESP32RTOS.ino`. The .ino file and the accompanying libraries should open in the IDE.

4. Use the library "esp32-hal-spi.h" for SPI. Can be obtained from doing the first task. 

5. Set the board to `ESP32 Dev Module`.

# Building 
After following the steps for installation, you can start by creating an account on your desired MQTT broker for testing purposes. It comes in many types of flavors, but our personal favorite and recommendation is CloudMQTT. Go to this link: https://www.cloudmqtt.com/. After you have created your account, prepare to gather the MQTT user, password, port and server because you need these in order to connect with your server. You also need to prepare your desired network name and password. It is very important to note that the ESP32 is itself an access point initally and that you would need to create its own server where the user can input their own MQTT server and Network for the ESP32 to connect to. In the initial stages of testing your software without implementing the ESP32 as its own access point, you would need to hardcode the information you have gathered in the beginning. 

# Background of Operation 

The Smart Charger initializes inputs and safety checks. After the safety check passes, it tries to connect to the wifi available. Then after being connected to the wifi it connects to the mqtt server. Initially the charger is in state A which means it is not plugged in. When it is plugged in but not charging, the charger is in state B. The wattmeter reads values such as Vrms, Irms, and active power. When it changes to state C which is at charging state, both relays will turn on. Pressing the button at certain amount of times will turn off the load, change the load, reset, and enter AP mode.  

# Usage
Smart Charger can be used to monitor the charging conditions of an electric vehicle. Online, an EV owner will be able to have control over the charger, for example they may ask for voltage levels and will be able to change the load going into the vehicle. It will be very useful in time as the number of electric vehicle users increase.  

## Connecting to WiFi

Upon first boot and after resets, the EVSE Smart Charger will start an access point (AP) to allow user to connect to a certain WiFI Access Point and MQTT broker.

1. On another device, connect to AP with SSID: `EVSESetup9B25B2`.
2. On a web browser, navigate to `192.168.10.10`.
3. Enter your valid WiFi and MQTT credentials on the form displayed. Then click 'Save.'
4. A success message should appear, the EVSE AP should disconnect, then the EVSE should connect to the WiFI network specified.

If there a failure, reset the EVSE networking information by pressing the reset button 11-12 times.

## MQTT Commands

The EVSE unit can be controlled remotely via MQTT commands. 