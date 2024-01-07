---
title: "Fast and Easy Way to Falsh Tasmota for Sonoff Devices"
description: ""
excerpt: ""
date: 2019-02-17T14:15:49-05:00
lastmod: 2023-01-26T22:43:45-05:00
draft: false
weight: 50
images: [sonoff.png]
categories: [Home Automation]
tags: [Sonoff, Tasmota]
contributors: []
pinned: false
homepage: false
---
Tosmota is a open source firmware that converts a black box Sonoff device to secure and extend its capabilities.  
There are several ways to flash a firmware to an ESP8266 based Sonoff devices. These include using Arduino IDE or PlatformIO. However these are slow and tedious methods (unless you want to edit several parts of the source code and recompile). If you are interested only in flashing a custom firmware and connect to Home Assistant or simpler, there is an easier and faster way to do that. 

**Update:** See simplified [Web UI configuration](http://venkat.ca/update-flashing-tasmota-firmware-gets-easier/) 

You need the following: 

A Sonoff device. You may buy from here. <https://www.itead.cc/smart-home/sonoff-wifi-wireless-switch.html>  
A serial programmer board. I use FT232RL based USB to Serial programmer adapter. [https://www.amazon.ca/gp/product/B01JG8H5U4/ref=oh\_aui\_search\_asin\_title?ie=UTF8&psc=1](https://www.amazon.ca/gp/product/B01JG8H5U4/ref=oh_aui_search_asin_title?ie=UTF8&psc=1)  
A set of 4 male-female jumper cables

**Steps:**

  1. We need a tool to flash the firmware. So, download the latest verison of Espeasy <https://github.com/letscontrolit/ESPEasy/releases> The current version is ESPEasy_mega-20190216.zip Unzip in a folder. 
  2. Download the most recent release Tasmota firmware. <https://github.com/arendst/Sonoff-Tasmota/releases> Download only sonff.bin This is good for most cases. (unless you need other capabilities/language interfaces)  
    Move this file in the same folder as _espeasy.exe_
  3. Open your Sonoff device and locate the Vcc, Rx, Tx, and GND terminals. Make connections to FT232RL as follows: Vcc <-> Vcc, Tx <-> Rx, Rx <-> Tx, and GND <-> GND. Ensure that that the Tx and Rx are reversed. What is transmitted by Tx in FT232RL should be Received by Sonoff and vice versa. 
  4. **This is very important:** Some serial programming adapters will have both 5V and 3.5V at Vcc, make sure that you connect ONLY 3.5 Vcc. Any higher voltage may fatally damage the Sonoff. 
  5. Press and hold Sonoff&#8217;s button as you connect the serial programmer board to the USB of your computer. Release the button after the board is powered on. This is meant to bring the ESP8266 chip to flashing mode. 
  6. Run _flashesp8266.exe_. Select the appropriate COM port. To find the correct port, go to your device manager and check under LPT and Serial Ports, find the COM port number of the USB Serial devices.
  7. Choose the appropriate bin file (say, sonoff.bin) and flash. If all connections are correct and you have put the Sonoff board in flashing mode, you will it being flashed. (if not go back and check your Tx and Rx connections and ensure that you are pressing and holding the Sonoff button as you connect the serial adapter to the USB port to enable the flashing mode).
  8. If all goes well you will see a flashed message. Unplug the serial adapter and replug it to reboot it. 
  9. Update: If you are using Tasmota v6.5 or above, there is a simplified procedure to configure the network. [Follow this write-up.](http://venkat.ca/update-flashing-tasmota-firmware-gets-easier/) You may ignore the instructions below. 
 10. Download the Termite program from <https://www.compuphase.com/software_termite.htm> It lets you to monitor and communicate with the Sonoff board through serial connection. Unzip it (and if you want you can permanently install it.) Run it. 
 11. Change the Settings to reflect the COM port you are connected to and set the baud rate to 115200. You will immediately see the communication from the serial port. 
 12. User _ssid1: <your router SSID>_. and _password1: <your router password>_ If you have access to another router, you can set it as well using _ssid2:_ and _password2:_ commands. You will immediately be connected to your network and your device ip address will be shown. 
 13. That is it!! Connect to the Tasmota flashed Sonoff device using http:// in a web browser. You can set all other options (such as MQTT) using the web interface. 

This is the fastest way to get your Sonoff flashed. This method is in no way restricted to flashing Tasmota firmware. You can also flash other precompiled binary firmware such as Espesy. There is no need for an arduino IDE, editing the source code to include your wireless credentials, compiling source code, etc. 

Remember, the ip address of your flashed Sonoff device is now set. If your router ever reboots and the DHCP assigns another IP address you cannot access the device through web interface without finding the new IP address from your router set up. The Tasmota web interface gives the device MAC address. I always write it down or make a label and stick it to the device. This will be helpful in easily identifying the device in your network. If you reserved the IP in your router, it will not change and easy to access of include it in any other program.
