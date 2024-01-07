---
title: "Services"
description: ""
lead: ""
date: 2023-01-27T08:13:14-05:00
lastmod: 2023-01-27T08:13:14-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "services-cf3c6130f3081c3297d8c0cd7885fe81"
weight: 309
toc: true
---
| Device                                                       | Quantity | Connection | Integration                                                  | Notes                                                        |
| ------------------------------------------------------------ | :------: | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [iOS App](https://itunes.apple.com/us/app/home-assistant-open-source-home-automation/id1099568401?mt=8) |    2     | NA         | Various                                                      | Mobile interface and presence detection in cell phone.  Wall-mounted Gen 2 iPAD for general use. |
| Android App                                                  |    4     | NA         | Various                                                      | 3 other mobile phones and 1 Samsung Tablet.                  |
| [AdGuard Home](https://adguard.com/en/adguard-home/overview.html) |    1     | Ethernet   | [AdGuard](https://www.home-assistant.io/integrations/adguard/) | Ad and malware blocking at the router level.  I recently moved from Pi-Hole to AdGuard.  Yet to see any difference. |
| [Pi-hole](https://pi-hole.net)                               |    1     | Ethernet   | [Pi-Hole Sensor](https://www.home-assistant.io/components/sensor.pi_hole/) | Configured in Raspberry Pi 2 connected directly to the primary router for ad blocking. (Deprecated, see above) |
| [AirVisual](https://www.home-assistant.io/integrations/airvisual/) |    1     | Ethernet   | [Airvisual](https://www.home-assistant.io/integrations/airvisual/) | Custom Shell script for managing Integration                 |
| [OpenUV](https://www.openuv.io/)                             |    1     | Cloud      | [Openuv](https://www.home-assistant.io/integrations/openuv/) | UV and Ozone data                                            |
| [Environment Canada](https://weather.gc.ca/index_e.html)     |    1     | Cloud      | [Environment Canada](https://www.home-assistant.io/integrations/environment_canada/) | Official weather service by Goverrnment of Canada            |
| [Dark Sky](https://darksky.net/)                             |    1     | Cloud      | [Dark Sky](https://www.home-assistant.io/integrations/darksky/) | See below                                                    |
| COVID-19                                                     |    1     | Cloud      | [Coronavirus](https://www.home-assistant.io/integrations/coronavirus/) | The data sourced from the [Johns Hopkins University](https://www.arcgis.com/apps/opsdashboard/index.html#/bda7594740fd40299423467b48e9ecf6) |


{{< callout context="note" title="Note" icon="info-circle" >}}
On March 31, 2020 Dark Sky was acquired by Apple (see, https://blog.darksky.net/dark-sky-has-a-new-home/) and is no longer allowing new API registrations. The Dark Sky API will continue to function for existing users through the end of 2021, but it is no longer possible to obtain an API key for new users.
{{< /callout >}}