---
title: "Flashing new firmware in Sonoff RF bridge"
description: ""
excerpt: ""
date: 2019-09-26T12:47:54-04:00
lastmod: 2019-09-26T12:47:54-04:00
draft: false
weight: 50
images: [sonoff_rf_bridge.jpg]
categories: [Home Automation]
tags: [Sonoff, Tasmota]
contributors: []
pinned: false
homepage: false
---
This follows my previous article on [Fast and Easy Way to Flash Tasmota Firmware for Sonoff Devices.](http://venkat.ca/fast-and-easy-way-to-flash-tasmota-firmware-for-sonoff-devices/) 

**Update:** See simplified [Web UI configuration.](http://venkat.ca/update-flashing-tasmota-firmware-gets-easier/) 

Sonoff RF bridge is a nice little gadget that converts 433 MHz (433.92 MHZ, to be precise) signals from RF senosors (such as motion and contact sensors) and switches (such as Key Fob clikcers, and buttons) to WiFi. This lets you to connect these low cost sensors, swithes, and blubs to the home automation system, such as the Home Assistant. 

Flashing RF Bridge is very similar to that of Sonoff Basic. Connect the FT232RL to the pins Tx, Rx, Vcc, and GND on the RF bridge to be flashed to Rx, Tx, Vcc and GND of the FT232RL adapter. (make sure that Tx is connected to Rx and Rx to Tx). 

Flip the switch (shown by arrow) to OFF position for flashing. 

Press and hold the button on the side (shown by Red arrow in the picture above) while booting to invoke the flashing mode. 

Then f[ollow the instructions](http://venkat.ca/fast-and-easy-way-to-flash-tasmota-firmware-for-sonoff-devices/) for flashing a Sonoff Basic. At the end of flashing, flip the switch back to ON position to make it function normally. Reboot the RF bridge by disconnecting the power and reconnecting it. 

If everything goes well, you will be able to log on to the device using the web interface. If will explain the procedure to integrate the Tasmota-flashed Sonoff RF bridge to Home Assistant in a future post.