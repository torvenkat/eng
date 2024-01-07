---
title: "Sensors"
description: ""
lead: ""
date: 2023-01-27T08:11:08-05:00
lastmod: 2023-01-27T08:11:08-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "sensors-7dece2e4755aa326ead8343940b0b492"
weight: 189
toc: true
---

| Device                                                       | Quantity | Connection | Integration                                            | Notes                                                        |
| ------------------------------------------------------------ | :------: | ---------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| [Nest Protect v2 Battery](https://amzn.to/2LJ0ACn)           |    3     | Wi-Fi      | [Nest](https://www.home-assistant.io/components/nest/) | Dual Smoke and CO Alarm.  One of the best fire/carbon monoxide alarms.  But recently Google has removed API access, and so the integration with Home Assistant is no longer working. |
| [Aqara Vibration Sensor](https://www.aqara.com/us/vibration_sensor.html) |    2     | Zigbee     | Binary Sensor                                          | I purchased it to automate (getting end of the cycle notificatoins) from my washing machine and dryer.  Not reliably automated yet. |

I wrote a script to blink Philips Hue bulbs when there is an alarm from Nest Protect.  Now that the Nest integration is broken, this has become useless. 