---
title: "Plants"
description: ""
lead: ""
date: 2023-01-27T08:11:56-05:00
lastmod: 2023-01-27T08:11:56-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "plants-f580818354b354f22844a56cb9b6d9c3"
weight: 219
toc: true
---
| Device                                                       | Quantity | Connection        | Integration                                                  | Notes                                                        |
| ------------------------------------------------------------ | :------: | ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Xiaomi Flower Care](https://xiaomi-mi.com/sockets-and-sensors/xiaomi-huahuacaocao-flower-care-smart-monitor/) |    2     | Bluetooth         | [ESPHome](https://www.home-assistant.io/integrations/esphome/); [plant](https://www.home-assistant.io/integrations/plant/) | See below                                                    |
| [Aquara sensor](https://www.gearbest.com/access-control/pp_626702.html?wid=1433363) |    1     | HUSBZB-1 (Zigbee) | [Zigbee](https://www.home-assistant.io/integrations/zigbee/) | Temperature, humidity, and occupancy sensors, used closer to plants for monitoring. |

I run a Bluetooth Tracker based on ESPHome in a ESP32. Under the platform  [xiaomi_hhccjcy01](https://esphome.io/components/sensor/xiaomi_hhccjcy01.html?highlight=xiaomi_hhccjcy01) this easily identifies the Xiami Flower Care sensors.  The [plant component](https://www.home-assistant.io/integrations/plant/) then merges the moisture, conductivity, light intensity, temperature and battery level for a plant into a single UI element.