# HomeAutomation_ESP8266
Home Automation System Using Arduino Uno &amp;  ESP8266 Module
In this project I'm going to make a home automation system using ESP8266 WiFi module and Arduino Uno. Using this we will be able to control lights, electric fan and other home appliances through a web browser using your PC or mobile. These AC mains appliances will be connected to relays which are controlled by the Arduino. ESP8266 and Arduino together acts as a Web Server and we will send control commands through a Web Browser like Google Chrome or Mozilla Firefox.

# ESP-01 ESP8266 Module

ESP-01 is the one of the most popular ESP8266 module available in the market. ESP8266 is a self contained SoC with integrated TCP/IP stack which helps any microcontroller having UART to access a wifi network. It can act as both WiFi access point as well as a WiFi client. It is pre-programmed with AT commands, so we can easily access and configure it using a microcontroller.

ESP8266 runs on 3.3V and its input pins are not 5V tolerant. So we need to reduce the 5V output of the Arduino Tx pin to 3.3V by using voltage dividing resistors to connect to Rx pin of ESP8266 module. Arduino TTL input pins will detect 3.3V as logic high, so we can directly connect 3.3V output of ESP8266 Tx to Arduino Rx pin.

# circuit diagram connection

Connect the VCC and CH_PD of the ESP8266 to the 3.3V output pin of Arduino. CH_PD is Chip Power Down pin, which is active low. So we will give 3.3V to it, which will enable the chip. Then connect the TXD pin of the ESP8266 with the digital pin 2 of the Arduino. Then make a voltage divider to make 3.3V for the RXD of the ESP8266 which is connected to the pin 3 of Arduino. Here we are using software UART through digital pins 2 & 3 of Arduino. Lastly, connect the ground of the ESP8266 with the ground of the Arduino.

Now we can connect relays to Arduino. Connect three relays to pins 11, 12 and 13 of the Arduino. Also connect 5V and ground from the Arduino to power the relay. Note that here I am using relay modules which having built in transistor driver. So don’t forget to add driver when you are using bare relays. We can connect AC devices to the output terminals of those relays. First connect one wire (Phase) of the AC source with the common terminal (COM) of all relays and the second wire (Neutral) of AC source to one terminal of AC devices. Then connect the other terminal of AC devices to the NO (Normally Open) terminal of relays.

# Explanation

HTML code uses the open source javascript library JQuery, so we need to obtain that. You can get it from this link and save it by right clicking on it. Save it in the same directory where you are going to save the above HTML code. Save the JQuery library file as the jquery.min and the full name of the file will be “jquery.min.js”.

Then copy above HTML code in a file and save it as an HTML file, say ‘control.html’.

Whenever a button is pressed in the web browser, a HTTP GET request is send to the Arduino-ESP8266 webserver to toggle a particular pin. In the Arduino code, it looks for the string “+IPD” again and again to check that if any request is coming or not. When it gets a request it reads the next character which is the connection id. Connection id is required to close the particular TCP connection after processing the request. Then it looks for the pin number to toggle by checking the character after the string “?pin=”. The Arduino then toggles that particular digital pin, which toggles the relay.

