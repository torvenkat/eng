---
title: "Cameras"
description: ""
lead: ""
date: 2023-01-27T08:11:19-05:00
lastmod: 2023-01-27T08:11:19-05:00
draft: false
images: []
menu:
  docs:
    parent: "configuration"
    identifier: "cameras-2d29a61abf836a7693ac57a6f725fa40"
weight: 199
toc: true
---
| Device                                                       | Quantity | Connection | Integration                                                  | Notes                                                        |
| ------------------------------------------------------------ | :------: | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Blink Hub                                                    |    1     | Wi-Fi      | [blink](https://www.home-assistant.io/integrations/blink/)   | Hub for Blink cameras                                        |
| [Blink XT2](https://www.amazon.ca/All-new-Blink-Outdoor-Security-included/dp/B07M5HWTZ9/ref=sr_1_3?keywords=blink+xt2&qid=1587943651&s=electronics&sr=1-3) |    2     | Blink Hub  | [blink](https://www.home-assistant.io/integrations/blink/)   | Outdoor cameras; also report temperature and battery status, albeit unreliably.  But very good battery life and motion detection. |
| [Yi Cam](https://www.amazon.ca/YI-Waterproof-Surveillance-Detection-Deterrent/dp/B01CW49AGG/ref=sr_1_3?crid=3ZAN4H0MBKIR&keywords=yi+camera+outdoor&qid=1587943783&s=electronics&sprefix=yi+cam%2Celectronics%2C156&sr=1-3) |    1     | Ethernet   | [ffmpeg](https://www.home-assistant.io/integrations/camera.ffmpeg/) | Outdoor; with open firmware (see below [1])                      |
| [Wyze Cam V3](https://www.wyze.com/products/wyze-cam?related_selling_plan=41618559008930) | 1 | WiFi | [ffmpeg](https://www.home-assistant.io/integrations/camera.ffmpeg/) | [2] |
| Shinobi                                                      |    1     | Etherrnet  |                                                              | Yet to integrate                                             |

[1] _Yi Camera uses [Yi-Hack-V4](https://github.com/TheCrypt0/yi-hack-v4) firmware.  I donated $5 and got the code to enable RTSP stream._

[2] _Wyze Cam V3 has built-in RTSP stream and easily integrates with HA._

### Previous

| Device                                                       | Quantity | Connection | Integration                                                  | Notes                                                        |
| ------------------------------------------------------------ | :------: | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Foscam F19803P](https://www.amazon.ca/FI9803P-Megapixel-1280x720p-Outdoor-Wireless/dp/B00M6TD4HO) |    1     | Ethernet   | [ffmpeg](https://www.home-assistant.io/integrations/camera.ffmpeg/) | Took a bit of effort to discover the rtsp feed, now is free from calling Foscam cloud.  This is now 6+ years old.  The model may not be available currently. |