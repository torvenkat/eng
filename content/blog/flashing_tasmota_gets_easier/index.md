---
title: "Update: Flashing Tasmota Firmware Gets Easier"
description: ""
excerpt: ""
date: 2019-03-22T14:17:13-04:00
lastmod: 2019-03-22T14:17:13-04:00
draft: false
weight: 50
images: [sonoff_rf_switch.jpg]
categories: [Home Automation]
tags: [Home Automation, Tasmota, Sonoff]
contributors: []
pinned: false
homepage: false
---
This updates the following posts: 

[Fast and Easy Way to Falsh Tasmota Firmware for Sonoff Devices](http://venkat.ca/fast-and-easy-way-to-flash-tasmota-firmware-for-sonoff-devices/) 

[Flashing New Firmware in Sonoff RF Bridge](http://venkat.ca/flashing-new-firmware-in-sonoff-rf-bridge/) 

<a href="https://github.com/arendst/Sonoff-Tasmota/releases/tag/v6.5.0" target="_blank" rel="noreferrer noopener" aria-label="Tasmota v6.5.0 (opens in a new tab)">Tasmota v6.5.0</a> has been released. This comes with the Web UI for configuration. If you are following my previous write-up to flash, you do not need Termite (or other serial communication monitors) to configure ssid and password during initial flash. 

You can ignore the instructions from [Step 9](http://venkat.ca/fast-and-easy-way-to-flash-tasmota-firmware-for-sonoff-devices/). Once you reboot the device after flashing, you will see a new network (something like SONOFF-XXXX) appearing. If you connect to that network, it will open the device configuration page automatically. This is usually 192.168.4.1. You can then configure the ssid and password from the Web UI. It is useful to also include a secondary ssid/password, (something that you have access to), just so in case you entered ssid1/password1 wrong, you will have another option to connect and modify.