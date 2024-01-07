---
title: "Max 6675 Thermocouple in Esphome"
description: ""
excerpt: ""
date: 2022-09-10T19:36:04-04:00
draft: false
weight: 50
images: []
categories: [Home Automation]
tags: [ESPhome]
contributors: []
pinned: false
homepage: false
---

Thermocouples are handy for accurate measurement at difficult to reach places or in liquids.  I set up one to measure the temperature of my aquarium so that I can get early warning if the heater fails in my tropical fish tank.  MAX6675 is very cheap and easily integrates with Esphome.  Here are the connections and code. 

## Connection:

| MAX6675 | ESP 8266 | D1 Mini terminal |
|:-------:|:--------:|:----------------:|
|   SO    |   MISO   |        D6        |
|   CS    |    CS    |        D8        |
|   SCK   |   CLK    |        D5        |
|   VCC   |          |       3.3V       |
|   GND   |   GND    |       GND        |

## Code

``` yaml
esphome:
  name: aquatemp
  platform: ESP8266
  board: d1_mini

# Enable logging
logger:

# Enable Home Assistant API
api:

ota:
  password: "****"

wifi:
  ssid: "****"
  password: "****"

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Aquatemp Fallback Hotspot"
    password: "****"

captive_portal:

# configuration entry
spi:
  miso_pin: D6
  clk_pin: D5

sensor:
  - platform: max6675
    name: "Aquarium Temperature"
    cs_pin: D8
    update_interval: 60s
```