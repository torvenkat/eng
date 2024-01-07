---
title: "Safety"
description: ""
lead: ""
date: 2023-01-27T08:10:40-05:00
lastmod: 2023-01-27T08:10:40-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "safety-2d72331ff643290bf9a976c4007d3877"
weight: 169
toc: true
---
| Device                                                       | Quantity | Connection        | Integration                                                  | Notes                                                        |
| ------------------------------------------------------------ | :------: | ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Nest Protect](https://amzn.to/2KwXltd)                      |    2     | Proprietary            | [Nest](https://www.home-assistant.io/integrations/nest/)     | [1] |
| [First Alert ZCOMBO-G](https://www.firstalertstore.com/store/products/z-wave-smoke-and-carbon-monoxide-alarm-zcombo-g.htm) | 3| HUSBZB-1  | Z-Wave | Easily connects by Zwave pairing | 
| [Ecowitt WH55 Water Leak Sensors](https://www.ecowitt.com/shop/goodsDetail/67#) | 2 | custom | [ecowitt](https://www.home-assistant.io/integrations/ecowitt/) | [2] |
| [Aqara Water Sensors](https://www.aqara.com/us/water_leak_sensor.html) |    2     | HUSBZB-1 (Zigbee) | [Zigbee](https://www.home-assistant.io/integrations/zigbee/) | Not very reliable                                            |
| [SmartThings Water Leak Sensor](https://www.samsung.com/us/smart-home/smartthings/sensors/samsung-smartthings-water-leak-sensor-gp-u999sjvlcaa/) |    1     | Zigbee            | SmartThings                                                  | Also includes temperature and humidity sensor.               |
| [Airthings](https://www.airthings.com/) | 1 | Bluetooth | [Airthings](https://www.home-assistant.io/integrations/airthings) | Indoor Radon, CO<sub>2</sub>, VOC, Temperature, humidity, and Pressure sensors. |

[1] _Nest detectors use a custom connectivity protocol called Weave and incorporate smoke and Carbon Monoxide Sensors. Currently not working reliably. Everytime the HA reboots, it need to be authorized manually._

[2] _Ecowitt sensors communicate via GW1000 Gateway (see [Hubs](../hubs) for details). As the connectivity to HA is local poling, this is fast and reliable._ 