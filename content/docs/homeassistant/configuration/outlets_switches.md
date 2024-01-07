---
title: "Outlets & Switches"
description: ""
lead: ""
date: 2023-01-27T08:10:11-05:00
lastmod: 2023-01-27T08:10:11-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "outlets_switches-6951718c9c4c10533cd8c3cca7024727"
weight: 149
toc: true
---


| Device                                                       | Quantity | Connection | Integration                                                  | Notes                                                        |
| ------------------------------------------------------------ | :------: | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Wemo Smart Plug](https://www.belkin.com/us/support-product?pid=01t80000002xFCbAAM) |    1     | Wi-Fi      | [WeMo](https://www.home-assistant.io/components/wemo/)       | Spare smart outlet, currently not being used.                |
| [TP Link Kasa Smart Plug](https://www.tp-link.com/ca/home-networking/smart-plug/hs110/) |    2     | Wi-Fi      | [TP-Link](https://www.home-assistant.io/integrations/tplink/), [Template Sensors](https://www.home-assistant.io/integrations/template/) | Power monitoring smart outlets; used in washing machine automation. *A newer model is available.* |
| [Sonoff Basic R2](https://sonoff.tech/product/wifi-diy-smart-switches/basicr2) |    6     | Wi-Fi      | [MQTT](https://www.home-assistant.io/integrations/mqtt/)     | Tasmota converted.                                           |
| White Label ESP8266 Smart Plugs                              |    2     | Wi-Fi      | [MQTT](https://www.home-assistant.io/integrations/mqtt/)     | Tasmota converted; energy monitoring.                        |
| [CE Smart Home LA-WF3](https://www.cesmarthome.com/LA-WF3.html) |    2     | Wi-Fi      | [MQTT](https://www.home-assistant.io/integrations/mqtt/)     | Tasmota converted                                            |
| [CE Smart Home LA-WF7](https://www.cesmarthome.com/LA-WF7.html) |    2     | Wi-Fi      | esphome                                                      | Similar to the above model, but report energy usage.         |

Kasa Smart plugs do not automatically report energy usage when using the TP-Link platform.  However, [template sensors](https://www.home-assistant.io/integrations/template/) can be created to extract these values.  When configured using **Integration** in the frontend, they are not very reliable.  I hard-coded their IP addresses in YAML mode and they are better.  

Power monitoring values from TP-Link Smart Plugs  can be extracted using template sensors.  Here is sample code: 

``` yaml
- platform: template

    sensors:

        switch_bed_warmer_amps:

            friendly_name_template: "{{ states.switch.bed_warmer}} Current"

            value_template: '{{ states.switch.bed_warmer.attributes["current_a"] | float }}'

            unit_of_measurement: 'A'

        switch_bed_warmer_watts:

            friendly_name_template: "{{ states.switch.bed_warmer}} Current Consumption"

            value_template: '{{ states.switch.bed_warmer.attributes["current_power_w"] | float }}'

            unit_of_measurement: 'W'

        switch_bed_warmer_total_kwh:

            friendly_name_template: "{{ states.switch.bed_warmer}} Total Consumption"

            value_template: '{{ states.switch.bed_warmer.attributes["total_energy_kwh"] | float }}'

            unit_of_measurement: 'kWh'

        switch_bed_warmer_volts:

            friendly_name_template: "{{ states.switch.bed_warmer}} Voltage"

            value_template: '{{ states.switch.bed_warmer.attributes["voltage"] | float }}'

            unit_of_measurement: 'V'

        switch_bed_warmer_today_kwh:

            friendly_name_template: "{{ states.switch.bed_warmer}} Today's Consumption"

            value_template: '{{ states.switch.bed_warmer.attributes["today_energy_kwh"] | float }}'

            unit_of_measurement: 'kWh'

```



CE Smart LA-WF7 is now running on esphome, but require an intermediate tasmota firmware through Tuya Convert hack.  Compated to TP Link Kasa smart plugs these are more reliable in reporting energy usage.  Esphome makes extracting energy data very easy, compared to using MQTT to connect and creating a series of template sensors.  At $10 apiece, these are of very good value. 