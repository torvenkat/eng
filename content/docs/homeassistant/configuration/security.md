---
title: "Security"
description: ""
lead: ""
date: 2023-01-27T08:10:26-05:00
lastmod: 2023-01-27T08:10:26-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "security-be421eedcfe716d68891b3b9d5988a85"
weight: 159
toc: true
---
| Device                                                       | Quantity | Connection           | Integration                                                  | Notes        |
| ------------------------------------------------------------ | :------: | -------------------- | ------------------------------------------------------------ | ------------ |
| [Schlage Connect Touchscreen Deadbolt](https://amzn.to/2KwXltd) |    2     | Z-Wave     | [Smarthings](https://www.home-assistant.io/integrations/smartthings/) |       |
| [Envisalink](https://www.eyezon.com/) | 1 | WiFi | [envisalink](https://www.home-assistant.io/integrations/envisalink/) | Integrates old Honeywell alarm panel and all its sensors to HA |
| [Aqara Contact Sensor](https://www.gearbest.com/access-control/pp_626703.html) |    2     | HUSBZB-1 (Zigbee)    | [Zigbee](https://www.home-assistant.io/integrations/zigbee/) |              |
| [Aquara PIR Motion Sensor](https://www.gearbest.com/alarm-systems/pp_659226.html?wid=1433363) |    2     | HUSBZB-1 (Zigbee)    | [Zigbee](https://www.home-assistant.io/integrations/zigbee/) |              |
| [Sonoff DW1 Contact Sensor](https://sonoff.tech/product/accessories/dw1) |    2     | Sonoff RF Bridge     | [MQTT](https://www.home-assistant.io/integrations/mqtt/)     |              |
| [Alfawise Contact Sensor](https://www.gearbest.com/access-control/pp_009265973897.html) |    3     | Sonoff RF Bridge     | [MQTT](https://www.home-assistant.io/integrations/mqtt/)     |              |
| [Alfawise PIR motion Sensor](https://www.gearbest.com/alarm-systems/pp_009990665530.html) |    4     | Sonoff RF Bridge     | [MQTT](https://www.home-assistant.io/integrations/mqtt/)     |              |
| [Sonoff motion Sensor](https://sonoff.tech/product/accessories/pir2) |    2     | Sonoff RF Bridge     | [MQTT](https://www.home-assistant.io/integrations/mqtt/)     |              |
| [Orvibo Motion Sensor](https://www.orvibo.com/en/product/bodysensor.html) |    1     | HUSBZB-1 (Zigbee)    | [Zigbee](https://www.home-assistant.io/integrations/zigbee/) | Not reliable |
| [Orvibo Contact Sensor](https://www.orvibo.com/en/product/doorsensor.html) |    1     | SmartThings (Zigbee) | SmartThings                                                  | Not reliable |

RF 433 MHz sensors are very cheap, typically about $5 and work reliably with Sonoff RF Bridge (Tasmota converted) and via MQTT integration. 

### Previous

| Device                                                       | Quantity | Connection           | Integration                                                  | Notes        |
| ------------------------------------------------------------ | :------: | -------------------- | ------------------------------------------------------------ | ------------ |
| [Orvibo Motion Sensor](https://www.orvibo.com/en/product/bodysensor.html) |    1     | HUSBZB-1 (Zigbee)    | [Zigbee](https://www.home-assistant.io/integrations/zigbee/) | Not reliable |
| [Orvibo Contact Sensor](https://www.orvibo.com/en/product/doorsensor.html) |    1     | SmartThings (Zigbee) | SmartThings                                                  | Not reliable |