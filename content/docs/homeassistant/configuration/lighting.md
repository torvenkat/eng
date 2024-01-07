---
title: "Lighting"
description: ""
lead: ""
date: 2023-01-27T08:09:43-05:00
lastmod: 2023-01-27T08:09:43-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "lighting-7935bbee8e9280896898e60231bc6cc2"
weight: 129
toc: true
---
| Device                                                       | Quantity | Connection           | Integration                                                  | Notes                                                        |
| ------------------------------------------------------------ | :------: | -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Leviton Decora DZMX1 ](https://www.leviton.com/en/products/dzmx1-1lz) |    4     | HUSBZB-1 (Z-Wave)    | [Z-Wave](https://www.home-assistant.io/integrations/zwave/)  | In-wall switch, dimmable. Can control LED, Incandescent, CFL, up to 1,000 W. A newer version available from Leviton. |
| [Leviton Decora DW6HD-1BZ](https://www.leviton.com/en/products/dw6hd-1bz) |    3     | Wi-Fi                | [Leviton Decora Wi-Fi](https://www.home-assistant.io/integrations/decora_wifi/) | In-wall switch, dimmable. Can control LED, Incandescent, CFL, up to 600 W. |
| [Philips Hue White](https://amzn.to/2LaUFTd)                 |    8     | Hue Hub (Zigbee)     | [Philips Hue Light](https://www.home-assistant.io/components/light.hue/) | Dimmable, single-CCT, *not sold anymore.*                    |
| [Philips Hue White & Color](https://www.amazon.ca/Ambiance-Equivalent-Dimmable-Compatible-Assistant/dp/B01M9AU8MB/ref=sr_1_16?keywords=hue+hub&qid=1586691613&sr=8-16) |    2     | Hue Hub (Zigbee)     | [Philips Hue Light](https://www.home-assistant.io/components/light.hue/) | Dimmable, single-CCT, *not sold anymore*                     |
| [Lutron Caseta Wireless Dimmer](https://amzn.to/2KwDJWc)     |    4     | Lutron Bridge        | [Lutron Caseta](https://www.home-assistant.io/components/lutron_caseta/) | Smart dimmer switches that do not require a neutral wire     |
| [Lutron Caseta Dimming Smart Plug PD-3PCL-WH-C](http://www.lutron.com/TechnicalDocumentLibrary/369987_ENG.pdf) |    2     | Lutron Bridge        | [Lutron Caseta](https://www.home-assistant.io/components/lutron_caseta/) | Controls two plug-in lamps.  Used for controlling old CFL torchieres. |
| [Lutron Caseta Pico Wireless Dimmer Switch](https://amzn.to/2Etw0HP) |    3     | Lutron Bridge        |                                                              | These are packaged remotes for the above dimmers, not directly integrated with HA. |
| [Cree Connected](https://amzn.to/2IpKAnZ)                    |    2     | Hue Hub (Zigbee)     | [Philips Hue Light](https://www.home-assistant.io/components/light.hue/) | Dimmable, single-CCT, *not sold anymore*                     |
| Ecosmart PAR 20, White                                       |    8     | SmartThings (Zigbee) | [Smarthings](https://www.home-assistant.io/integrations/smartthings/) | Warm-white, dimmable. I bought it on a clearance at CDN $5 apiece.  *May not be available anymore.* |
| Ecosmart PAR 20, Color                                       |    2     | SmartThings (Zigbee) | [Smarthings](https://www.home-assistant.io/integrations/smartthings/) | RGB, dimmable. I bought it on a clearance at CDN $6 apiece.  *May not be available anymore.* |
| [GE Link Smart LED bulb](https://www.amazon.ca/GE-Wireless-Smart-PSB19-SW27-Equivalent/dp/B00NOL16K0) |    2     | HUSBZB-1 (Zigbee)    | [Philips Hue Light](https://www.home-assistant.io/components/light.hue/) | Dimmable, single-CCT, not very reliable, *not sold anymore.* |
| [Nanoleaf Aurora](https://nanoleaf.me/en/consumer-led-lighting/products/smarter-series/nanoleaf-light-panels-smarter-kit/) |    1     | Wi-Fi                | [Nanoleaf](https://www.home-assistant.io/integrations/nanoleaf/) | Decorative RGB panels.                                       |
| [Generic RGB controller](https://www.alibaba.com/product-detail/Mini-RGB-Wifi-Controller-for-LED_62261692811.html?spm=a2700.7724857.normalList.12.217949dfxfding&s=p&fullFirstScreen=true), HF-LPB100 Chipset |    1     | Wi-Fi                | [Flux LED](https://www.home-assistant.io/integrations/flux_led/) | Cheap ($5) RGB LED string controller used for decorative skylight.  Will migrate to Tasmota some day. |
| [TP Link HS200](https://www.tp-link.com/ca/home-networking/smart-plug/hs200/) |    2     | Wi-Fi                | [TP-Link](https://www.home-assistant.io/integrations/tplink/) | Non-dimmable, in-wall switches                               |
